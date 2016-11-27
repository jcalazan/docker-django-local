docker-django-local
===================

Dockerfiles to create images for use in local Django development environments.

Designed to be used with [Docker Compose](https://docs.docker.com/compose/), it will make things a lot easier.

I took most of these Dockerfiles from existing projects and modified them to work for my setup.

Here's a sample Django application that uses these Docker images: https://github.com/jcalazan/youtube-audio-dl

## Images Info

- **base** - Ubuntu 14.04 with commonly used packages for Django/Python development.
- **postgresql** - PostgreSQL 9.6 database (default username/password is docker/docker).
- **django** - Not much difference from the base image except port 80 is exposed and contains a few additional packages/libraries.
- **rabbitmq** - RabbitMQ message broker usually used with Celery. 

## Docker Registry

You can pull these images directly from the Docker Registry: https://hub.docker.com/u/jcalazan/

This repo is configured for automated builds.

## Sample ```docker-compose.yml``` Configuration

```
postgresql:
  image: jcalazan/postgresql
  environment:
    - POSTGRESQL_DB=youtubeadl
    - POSTGRESQL_USER=youtubeadl
    - POSTGRESQL_PASSWORD=password
  volumes:
    - ~/dockerfiles/youtube-audio-dl/postgresql:/var/lib/postgresql
  ports:
    - "5432:5432"

rabbitmq:
  image: jcalazan/rabbitmq
  ports:
    - "15672:15672"

# NOTES:
#   - The C_FORCE_ROOT variable allows celery to run as the root user.
celery:
  image: jcalazan/django
  environment:
    - C_FORCE_ROOT=true
    - DATABASE_HOST=postgresql
    - BROKER_URL=amqp://guest:guest@rabbitmq//
  working_dir: /youtube-audio-dl
  command: bash -c "sleep 3 && celery -A youtubeadl worker -E -l info --concurrency=3"
  volumes:
    - .:/youtube-audio-dl
    - ~/dockerfiles/youtube-audio-dl/python:/usr/local/lib/python2.7
    - ~/dockerfiles/youtube-audio-dl/bin:/usr/local/bin
  links:
    - postgresql
    - rabbitmq

# NOTES:
#   - The C_FORCE_ROOT variable allows celery to run as the root user.
flower:
  image: jcalazan/django
  environment:
    - C_FORCE_ROOT=true
    - DATABASE_HOST=postgresql
    - BROKER_URL=amqp://guest:guest@rabbitmq//
  working_dir: /youtube-audio-dl
  command: bash -c "sleep 3 && celery -A youtubeadl flower --port=5555"
  volumes:
    - .:/youtube-audio-dl
    - ~/dockerfiles/youtube-audio-dl/python:/usr/local/lib/python2.7
    - ~/dockerfiles/youtube-audio-dl/bin:/usr/local/bin
  ports:
    - "5555:5555"
  links:
    - postgresql
    - rabbitmq

django:
  image: jcalazan/django
  environment:
    - DATABASE_HOST=postgresql
    - BROKER_URL=amqp://guest:guest@rabbitmq//
  working_dir: /youtube-audio-dl
  command: bash -c "sleep 3 && python manage.py runserver_plus 0.0.0.0:80" 
  volumes:
    - .:/youtube-audio-dl
    - ~/dockerfiles/youtube-audio-dl/python:/usr/local/lib/python2.7
    - ~/dockerfiles/youtube-audio-dl/bin:/usr/local/bin
  ports:
    - "80:80"
  links:
    - postgresql
    - rabbitmq
```

#### A few things to note about this sample configuration:

- Under `volumes:`, local directories are mapped to the containers.  It expects `docker-compose.yml` to be in the root project directory.  Python packages are also mapped from the local directory to make the image more reusable (i.e. no need to rebuild the images every time you add a new package to your project).
- For the `youtube-audio-dl` project, the `manage.py` file is in the project root, that's why I set that path as the `working_dir`.
- You can run Django management commands inside the `django` container by prepending `fig run django` (e.g. `fig run django python manage.py migrate`).
- By default, everything run as `root` in the Docker containers.
- The `sleep` part in the command is to make sure the PostgreSQL service is ready to accept the connections before running a command that depends on it (see https://github.com/docker/compose/issues/374).
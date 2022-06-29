docker-django-local
===================

Dockerfiles to create images for use in local Django development environments.

Designed to be used with [Docker Compose](https://docs.docker.com/compose/), it will make things a lot easier.

I took most of these Dockerfiles from existing projects and modified them to work for my setup.


## Images Info

- **base** - Ubuntu 16.04 with commonly used packages for Django/Python development.
- **postgresql** - PostgreSQL 9.6 database (default username/password is docker/docker).
- **django** - Not much difference from the base image except port 80 is exposed and contains a few additional packages/libraries.
- **rabbitmq** - RabbitMQ message broker usually used with Celery. 


#### A few things to note about this sample configuration:

- Under `volumes:`, local directories are mapped to the containers.  It expects `docker-compose.yml` to be in the root project directory.  Python packages are also mapped from the local directory to make the image more reusable (i.e. no need to rebuild the images every time you add a new package to your project).
- For the `youtube-audio-dl` project, the `manage.py` file is in the project root, that's why I set that path as the `working_dir`.
- You can run Django management commands inside the `django` container by prepending `docker-compose run django` (e.g. `docker-compose run django python manage.py migrate`).
- By default, everything run as `root` in the Docker containers.
- The `sleep` part in the command is to make sure the PostgreSQL service is ready to accept the connections before running a command that depends on it (see https://github.com/docker/compose/issues/374).

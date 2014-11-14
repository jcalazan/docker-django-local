docker-django-local
===================

Status: Work in progress

Dockerfiles to create images for use in local Django development environments.

Designed to be used with [Fig](https://github.com/docker/fig), it will make things a lot easier.

I took most of these Dockerfiles from existing projects and modified them to work for my setup.

## Images Info

**Note:** You should build the **base** image first as other images inherit from it.

- **base** - Ubuntu 12.04 with commonly used packages for Django/Python development.
- **postgresql** - PostgreSQL 9.1 database (default username/password is docker/docker).
- **django** - Not much difference from the base image except port 80 is exposed and contains a few additional packages/libraries.
- **rabbitmq** - RabbitMQ message broker usually used with Celery. 

More info in the role folders (coming soon).

## Docker Registry

You can pull these images directly from the Docker Registry: https://hub.docker.com/u/jcalazan/

This repo is configured for automated builds.

## Getting Started

<coming soon>

## Sample ```fig``` Configuration

```
postgresql:
  image: jcalazan/postgresql
  environment:
    - POSTGRESQL_DB=calazanblog
    - POSTGRESQL_USER=calazanblog
    - POSTGRESQL_PASSWORD=password
  volumes:
    - /dockerfiles/calazan-blog/postgresql:/var/lib/postgresql
  ports:
    - "5432:5432"

django:
  image: jcalazan/django
  environment:
    - DJANGO_SETTINGS_MODULE=calazanblog.settings.local
    - DATABASE_NAME=calazanblog
    - DATABASE_USER=calazanblog
    - DATABASE_PASSWORD=password
    - DATABASE_HOST=postgresql
  working_dir: /calazan-blog
  command: >
    bash -c "sleep 2 && python manage.py runserver 0.0.0.0:80"
  volumes:
    - /dockerfiles/calazan-blog/python:/usr/local/lib/python2.7
    - ../calazan-blog:/calazan-blog
  ports:
    - "80:80"
  links:
    - postgresql
```

## Resources

- https://registry.hub.docker.com/u/orchardup/postgresql/

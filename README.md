docker-django-local
===================

Dockerfiles to create images for use in local Django development environments.

Designed to be used with [Fig](https://github.com/docker/fig), it will make things a lot easier.

NOTE: Work in progress, more info coming soon.

## Images Info

**Note:** You should build the **base** image first as other images inherit from it.

- **base** - Ubuntu 12.04 with commonly used packages for Django/Python development
- **postgresql** - PostgreSQL 9.1 (port 5432 exposed)
- **django** - Not much difference from the base image except port 80 is exposed
- **rabbitmq** - <coming soon>

## Getting Started

<coming soon>

## Resources

- https://registry.hub.docker.com/u/orchardup/postgresql/
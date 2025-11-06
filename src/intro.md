
# Distributed system design

This is a book like documentation of a inventory system.

This inventory distributed system has following parts. And each part of these microservices has different technic stack.

<!-- toc -->

## Auth Service

This micro service is composed by frontend part and backend part.

The backend part is powered by [Django](https://www.djangoproject.com/). Database is using [Postgresql@17](https://www.postgresql.org/), and docker version is on [Postgresql Docker](https://hub.docker.com/_/postgres).

The frontend part is powered by [Svelte 5.41.0](https://svelte.dev/docs) and [Svelte Kit 2.47.1](https://svelte.dev/docs/kit/introduction), javascript runtime is [Bun](https://bun.com/docs).

For more details, go to [here](./auth_service/intro.md).



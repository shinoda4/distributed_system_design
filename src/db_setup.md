# Database Setup

## Auth Service

### Postgres

```shell
sudo docker run --name auth-service-postgres -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d postgres
```

### Redis

```shell
sudo docker run --name auth-service-redis -p 6379:6379 -d redis
```

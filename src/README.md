

# distributed system design

- Auth Service

Backend: https://github.com/shinoda4/auth_service.git

API: https://github.com/shinoda4/auth_service_api.git

Frontend: https://github.com/shinoda4/auth_service_svelte.git

- Product Service

- Inventory Service

- Order Service

- Shipment/Transaction Service

- Procurement Service

- Analytics/BI Service

- Notification Service

## Database Stratup

### Auth Service

#### Postgres

```shell
sudo docker run --name auth-service-postgres -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d postgres
```

#### Redis

```shell
sudo docker run --name auth-service-redis -p 6379:6379 -d redis
```

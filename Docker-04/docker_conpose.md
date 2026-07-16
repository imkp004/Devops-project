# Docker Compose - Retail Store Sample App

Run a multi-container microservices retail app (10 services: APIs, databases, messaging, UI) with Docker Compose.

## Services

| Service | Image |
|---|---|
| cart | public.ecr.aws/aws-containers/retail-store-sample-cart:1.3.0 |
| carts-db | amazon/dynamodb-local:1.20.0 |
| catalog | public.ecr.aws/aws-containers/retail-store-sample-catalog:1.3.0 |
| catalog-db | mariadb:10.9 |
| checkout | public.ecr.aws/aws-containers/retail-store-sample-checkout:1.3.0 |
| checkout-redis | redis:6.0-alpine |
| orders | public.ecr.aws/aws-containers/retail-store-sample-orders:1.3.0 |
| orders-db | postgres:16.1 |
| rabbitmq | rabbitmq:3-management |
| ui | public.ecr.aws/aws-containers/retail-store-sample-ui:1.3.0 |

## 1. Install Docker Compose (if needed)

```bash
sudo mkdir -p /usr/local/lib/docker/cli-plugins
wget https://github.com/docker/compose/releases/latest/download/docker-compose-linux-x86_64 -O docker-compose
chmod +x docker-compose
sudo mv docker-compose /usr/local/lib/docker/cli-plugins/docker-compose
docker compose version
```

## 2. Get the Compose File and Start Services

```bash
mkdir demo-compose && cd demo-compose
wget https://github.com/aws-containers/retail-store-sample-app/releases/download/v1.3.0/docker-compose.yaml

export DB_PASSWORD='mydbkalyan101'

docker compose up -d
```

## 3. Test the App

```
http://<EC2-Instance-Public-IP>:8888
```

## 4. Common Commands

```bash
# List running services
docker compose ps

# Stop / start a service
docker compose stop orders
docker compose start orders

# Restart a service
docker compose restart cart

# Logs
docker compose logs -f checkout

# Resource stats
docker compose stats

# Running processes in a container
docker compose top ui

# Shell into a container
docker compose exec ui sh
```

## 5. Change a Config Value (Example)

Edit `docker-compose.yaml` — under the `ui` service's `environment` section, add:

```yaml
- RETAIL_UI_THEME=green
```

Apply the change:

```bash
docker compose up -d --force-recreate ui
```

Verify:

```bash
docker compose exec ui sh
env | grep RETAIL
exit
```

Refresh `http://<EC2-Public-IP>:8888` — the UI theme should now be green.

## 6. Clean Up

```bash
docker compose down
docker system prune -a --volumes -f
```

## Reference

- [Retail Store Sample App (GitHub)](https://github.com/aws-containers/retail-store-sample-app)

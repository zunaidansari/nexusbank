# NexusBank

A banking platform built as a set of Spring Boot microservices, with an API gateway, service discovery, centralised configuration, event-driven messaging and a full observability stack.

## Architecture

| Module | Role |
|---|---|
| `configserver` | Centralised configuration for all services (per-environment configs live in the [yourbank-config](https://github.com/zunaidansari/yourbank-config) repo) |
| `eurekaserver` | Service discovery |
| `gatewayserver` | Single entry point and routing for all client requests |
| `accounts` | Customer and account management |
| `cards` | Card management |
| `loans` | Loan management |
| `message` | Notification service, consuming events through Spring Cloud Stream on Kafka |

## Tech stack

- Java, Spring Boot, Spring Cloud (Config, Eureka, Gateway, Stream)
- Apache Kafka for asynchronous messaging
- Keycloak for authentication and authorisation
- Docker and Docker Compose, with images built through Jib
- Prometheus, Grafana, Loki and Tempo for metrics, logs and traces

## Running with Docker Compose

The Compose setup in `docker-compose/default` starts all services together with Kafka, Keycloak and the observability stack:

```bash
cd docker-compose/default
docker compose up -d
```

## Running locally from an IDE

1. Clone the repository and open it in an IDE such as IntelliJ IDEA.
2. Let the IDE import the Maven dependencies for each module.
3. Build each Maven module to confirm everything compiles.
4. Start the services in this order:
   1. Config Server
   2. Eureka Server
   3. Cards
   4. Loans
   5. Accounts
   6. Gateway Server
5. Call the APIs through the Gateway Server, using Postman or any HTTP client.

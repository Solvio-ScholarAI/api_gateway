# API Gateway Service

Spring Cloud Gateway implementation for ScholarAI microservices platform. This service acts as a single entry point for all client requests, providing routing, load balancing, and API aggregation.

## Features

- **Intelligent Routing**: Route requests to appropriate microservices based on path patterns
- **Service Discovery**: Integration with Eureka for dynamic service discovery
- **Load Balancing**: Client-side load balancing with Caffeine cache
- **API Documentation**: Aggregated Swagger/OpenAPI documentation from all services
- **CORS Support**: Configurable CORS policies for frontend integration
- **Health Monitoring**: Actuator endpoints for health checks and metrics
- **Reactive Architecture**: Built on Spring WebFlux for high performance

## Tech Stack

- Java 21
- Spring Boot 3.5.4
- Spring Cloud Gateway
- Spring Cloud Netflix Eureka
- OpenAPI/Swagger
- Docker & Docker Compose

## Prerequisites

- Java 21+
- Maven 3.9+ (or use included wrapper)
- Docker & Docker Compose (for containerized deployment)

## Quick Start

### Local Development

```bash
# Build the application
./scripts/local.sh build

# Run the application
./scripts/local.sh run

# View logs
./scripts/local.sh logs

# Stop the application
./scripts/local.sh stop
```

### Docker Deployment

```bash
# Build Docker image
./scripts/docker.sh build

# Run container
./scripts/docker.sh run

# View logs
./scripts/docker.sh logs

# Stop container
./scripts/docker.sh stop
```

## Configuration

The application supports multiple profiles:

- **local**: For local development (port 8989)
- **docker**: For Docker deployment with Eureka integration
- **prod**: For production with enhanced security and monitoring

Set the profile using:
```bash
export SPRING_PROFILES_ACTIVE=docker
```

## API Documentation

Once running, access the aggregated API documentation at:
- Swagger UI: http://localhost:8989/swagger-ui.html
- OpenAPI JSON: http://localhost:8989/v3/api-docs

## Health Check

Monitor service health at:
- http://localhost:8989/actuator/health

## Routing Configuration

The gateway routes requests based on path patterns:

- `/api/users/**` → User Service
- `/api/notifications/**` → Notification Service  
- `/api/papers/**` → Project Service
- `/api/v1/extraction/**` → Project Service (Extractor)

## Environment Variables

See `env.example` for available configuration options.

## Scripts

- `scripts/local.sh` - Local development management
- `scripts/docker.sh` - Docker container management

## Project Structure

```
api_gateway/
├── src/
│   ├── main/
│   │   ├── java/org/solace/scholar_ai/api_gateway/
│   │   │   ├── ApiGatewayApplication.java
│   │   │   └── config/
│   │   │       └── SwaggerConfig.java
│   │   └── resources/
│   │       ├── application.yml
│   │       ├── application-local.yml
│   │       ├── application-docker.yml
│   │       └── application-prod.yml
│   └── test/
├── scripts/
│   ├── docker.sh
│   └── local.sh
├── Dockerfile
├── docker-compose.yml
├── docker-compose.prod.yml
├── pom.xml
└── README.md
```

## License

MIT License
# Retail Store Sample App (DevOps Edition)

A polyglot microservices application demonstrating modern containerization and DevOps practices. This project has been customized to showcase a complete DevOps lifecycle including Docker containerization, CI/CD with Jenkins, and deployment to Kubernetes.

## 🏗️ Architecture

The application consists of several decoupled microservices, each built with different technologies and databases to demonstrate a realistic, heterogeneous environment.

| Component | Language | Framework | Database | Description |
|-----------|----------|-----------|----------|-------------|
| **UI** | Java | Spring Boot | - | Storefront/BFF (Backend for Frontend). Aggregates data from other services. |
| **Catalog** | Go | - | MySQL | Manages products and categories. |
| **Cart** | Java | Spring Boot | DynamoDB | Manages user shopping carts. |
| **Orders** | Java | Spring Boot | PostgreSQL | Manages order processing. |
| **Checkout** | Node.js | NestJS | Redis | Orchestrates the checkout flow. |

## 🚀 Technologies

*   **Containerization**: Docker (Multi-stage builds, Distroless images)
*   **Orchestration**: Kubernetes (Planned)
*   **CI/CD**: Jenkins (Planned)
*   **Messaging**: RabbitMQ (for async processing)
*   **Databases**: MySQL, PostgreSQL, DynamoDB (Local), Redis

## 🛠️ Local Development

All services have been containerized using production-ready Dockerfiles located in their respective directories.

### Prerequisites
*   Docker
*   Make (optional, if Makefile exists)

### Building and Running Services

You can build and run each service independently using Docker.

#### 1. Catalog Service (Go)
```bash
cd src/catalog
docker build -t catalog-service .
docker run -d -p 8080:8080 catalog-service
```

#### 2. Cart Service (Java)
```bash
cd src/cart
docker build -t cart-service .
docker run -d -p 8080:8080 cart-service
```

#### 3. Orders Service (Java)
```bash
cd src/orders
docker build -t orders-service .
docker run -d -p 8080:8080 orders-service
```

#### 4. Checkout Service (Node.js)
```bash
cd src/checkout
docker build -t checkout-service .
docker run -d -p 8080:8080 checkout-service
```

#### 5. UI Service (Java)
```bash
cd src/ui
docker build -t ui-service .
# Note: UI requires other services to be running. Update .env or pass env vars accordingly.
docker run -d -p 8080:8080 ui-service
```

## 🔒 Security

This project follows container security best practices:
*   **Distroless Images**: Using `gcr.io/distroless` base images to minimize attack surface.
*   **Non-Root Users**: All containers run as non-root users.
*   **Multi-Stage Builds**: Build tools and dependencies are excluded from the final runtime images.

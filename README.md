# payment-service-resilient

A complete Spring Boot 3.x microservice for processing debit and credit card payments with resilience features:

## ✅ Features
- Circuit Breaker using **Resilience4j**
- Kafka-based **asynchronous retry** for failed payments
- PostgreSQL integration to **persist failed attempts**
- Observability via **Prometheus** & **Grafana**
- Dockerized services for local development

---

## 📁 Project Structure

```
payment-service-resilient/
├── src/
│   └── main/
│       ├── java/
│       │   └── com/example/paymentservice/
│       │       ├── controller/
│       │       │   └── PaymentController.java
│       │       ├── consumer/
│       │       │   └── PaymentRetryConsumer.java
│       │       ├── entity/
│       │       │   └── FailedPayment.java
│       │       ├── repository/
│       │       │   └── FailedPaymentRepository.java
│       │       ├── service/
│       │       │   └── PaymentService.java
│       │       └── PaymentServiceApplication.java
│       └── resources/
│           ├── application.yml
│           └── prometheus.yml
├── docker-compose.yml
├── grafana-dashboard.json
└── README.md
```

---

## 🚀 Setup Instructions

### 1. Prerequisites
- Java 17+
- Docker + Docker Compose

### 2. Run Docker Services
```bash
docker-compose up -d
```

### 3. Start Spring Boot App
```bash
./mvnw spring-boot:run
```

### 4. Access Tools
- **Kafka UI** (optional if added)
- **Prometheus**: [http://localhost:9090](http://localhost:9090)
- **Grafana**: [http://localhost:3000](http://localhost:3000)
  - Login: `admin / admin`
  - Import `grafana-dashboard.json`

### 5. Test API
```bash
curl -X POST 'http://localhost:8080/api/payments/debit?orderId=123'
curl -X POST 'http://localhost:8080/api/payments/credit?orderId=456'
```

---

## 🔒 Health Endpoints
- [http://localhost:8080/actuator/health](http://localhost:8080/actuator/health)
- [http://localhost:8080/actuator/prometheus](http://localhost:8080/actuator/prometheus)

---

## 📦 Kafka Retry Logic
Failed payments are:
- Logged in PostgreSQL
- Sent to Kafka topic `payment-retry`
- Retried by consumer service asynchronously

---

## 📄 License
MIT License — free to use and adapt.

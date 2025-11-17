# FraudBuster - Fraud Detection & Review Analysis System

A cloud-distributed microservices system for detecting fraudulent and bot-generated product reviews using machine learning models, gRPC communication, and distributed caching.

## 📋 Overview

FraudBuster analyzes Amazon product reviews to identify generic, bot-generated, and fraudulent reviews using pretrained BERT models. The system features a microservices architecture with 6 custom services communicating via gRPC, backed by Redis caching and MongoDB persistence.

## 🏗️ Architecture

**Microservices:**
- `flask-app` - HTTP API Gateway & Web Frontend (Port 5000)
- `review-classifier` - ML-powered review classification using BERT (Port 50051)
- `relevance-scorer` - Review relevance scoring service (Port 50052)
- `scraper` - Amazon product review scraper (Port 50053)
- `mongo-store` - gRPC database writer service (Port 50054)
- `scheduler` - Background task orchestrator

**Infrastructure:**
- Redis - Distributed cache layer (Port 6379)
- MongoDB 7 - Persistent data storage (Port 27017)

**Communication:** All microservices communicate via gRPC with Protocol Buffers

## 📁 Project Structure

```
.
├── dataset/                    # Training dataset for review-classifier model
├── flask-app/                  # API Gateway microservice
├── k8s/                        # Kubernetes deployment files
│   ├── run_fraudbuster(win).bat    # Windows deployment script
│   └── run_fraudbuster(mac).sh     # Mac/Linux deployment script
├── mongo-store/                # Database writer microservice
├── protos/                     # gRPC Protocol Buffer definitions
├── relevance-scorer/           # Review scoring microservice
├── review-classifier/          # ML classification microservice
├── scheduler/                  # Task orchestration microservice
├── scraper/                    # Web scraping microservice
├── docker-compose.yml          # Docker Compose configuration
└── README.md                   # This file
```

## 🚀 Quick Start

### Prerequisites

- Docker Desktop (version 20.10+)
- Docker Compose (version 2.0+)
- (Optional) Minikube + kubectl for Kubernetes deployment

### Installation

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd <repository-folder>
   ```

2. **Pull all service images from Docker Hub:**
   ```bash
   docker-compose pull
   ```
   *Wait time: ~2-5 minutes depending on internet speed*

3. **Start all services:**
   ```bash
   docker-compose up --build
   ```
   *Services will initialize in ~30 seconds*

4. **Verify all containers are running:**
   ```bash
   docker ps
   ```
   *Expected: 8 running containers*

5. **Access the application:**
   ```
   http://localhost:5000
   ```

### Basic Commands

**View logs:**
```bash
docker-compose logs -f <service-name>
# Example: docker-compose logs -f flask-app
```

**Restart a specific service:**
```bash
docker-compose restart <service-name>
```

**Stop all services:**
```bash
docker-compose down
```

**Update to latest images:**
```bash
docker-compose pull
docker-compose up -d --force-recreate
```

## ☸️ Kubernetes Deployment (Alternative)

For Kubernetes/Minikube deployment:

1. **Ensure Minikube is running:**
   ```bash
   minikube start
   ```

2. **Navigate to k8s folder:**
   ```bash
   cd k8s
   ```

3. **Run the deployment script:**

   **Windows:**
   ```bash
   run_fraudbuster(win).bat
   ```

   **Mac/Linux:**
   ```bash
   chmod +x run_fraudbuster(mac).sh
   ./run_fraudbuster(mac).sh
   ```

4. **Check pod status:**
   ```bash
   kubectl get pods -w
   ```
   *Wait until all pods show STATUS: Running*

5. **Access the service:**
   ```bash
   minikube service flask-app-service
   ```

## 🧪 Testing

For comprehensive testing instructions, refer to the **GROUPNN_INSTRUCTIONS.pdf** file included in the submission.

The PDF contains:
- Detailed testing scenarios
- Expected outputs for each test case
- Troubleshooting guide
- Performance benchmarks

## 🛠️ Built With

- **Backend:** Flask, Python 3.10+
- **ML Models:** BERT (Pretrained Transformers)
- **Communication:** gRPC, Protocol Buffers
- **Databases:** MongoDB 7, Redis
- **Orchestration:** Docker Compose, Kubernetes
- **Container Registry:** Docker Hub

## 📦 Docker Images

All microservice images are hosted on Docker Hub:

- `caffeinatedkong/flask-app:latest`
- `caffeinatedkong/review-classifier:latest`
- `caffeinatedkong/relevance-scorer:latest`
- `caffeinatedkong/scraper:latest`
- `caffeinatedkong/mongo-store:latest`
- `caffeinatedkong/scheduler:latest`

Public repositories available at: https://hub.docker.com/u/caffeinatedkong

## 🔧 Configuration

All services are pre-configured via `docker-compose.yml`. No manual configuration required for basic deployment.

**Environment Variables:**
- `PYTHONUNBUFFERED=1` - Real-time Python logging
- Service hostnames auto-configured via Docker network

## 📊 Service Ports

| Service            | Port  | Protocol |
|--------------------|-------|----------|
| flask-app          | 5000  | HTTP     |
| review-classifier  | 50051 | gRPC     |
| relevance-scorer   | 50052 | gRPC     |
| scraper            | 50053 | gRPC     |
| mongo-store        | 50054 | gRPC     |
| redis              | 6379  | TCP      |
| mongo              | 27017 | TCP      |

## 🐛 Troubleshooting

**Port conflicts:**
```bash
# Check if ports are in use
netstat -an | findstr "5000"

```

**Services not starting:**
```bash
# Check service logs
docker-compose logs <service-name>

```

**Old cached images:**
```bash
docker-compose down
docker rmi -f caffeinatedkong/<service-name>:latest
docker-compose pull
docker-compose up -d
```

## 📝 Project Information

**Course:** CSC3104 - Cloud and Distributed Computing  
**Institution:** Singapore Institute of Technology  
**Submission Date:** November 16, 2025

## 👥 Contributors

Group 09 - FraudBuster Team

## 📄 License

This project is submitted as part of academic coursework.

---

For detailed testing instructions and submission requirements, please refer to **GROUP09_INSTRUCTIONS.pdf**.

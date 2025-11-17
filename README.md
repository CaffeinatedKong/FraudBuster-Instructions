# FraudBuster - Fraud Detection & Review Analysis System

A cloud-distributed microservices system for detecting fraudulent and bot-generated product reviews using machine learning models, gRPC communication, and distributed caching.

---

## 🚀 Quick Start

### Prerequisites

Ensure you have the following installed on your machine:
- Docker Desktop (version 20.10+)
- Docker Compose (version 2.0+)
- (Optional) Minikube + kubectl for Kubernetes deployment

### Installation

1. **Clone the repository:**

```bash
git clone <repository-url>
cd <repository-folder>
Pull all service images from Docker Hub:

bash
Copy code
docker-compose pull
Wait time: ~2-5 minutes depending on internet speed

Start all services:

bash
Copy code
docker-compose up --build
Services will initialize in ~30 seconds

Verify all containers are running:

bash
Copy code
docker ps
Expected: 8 running containers

Access the application:

Open your browser and go to:

arduino
Copy code
http://localhost:5000
📸 Screenshots of the Application
Once you’ve accessed the application, wait for the scraper to finish. You’ll see the results once scraping is complete.

Insert image of the application interface when running, e.g., loading page or results page.

🧪 Testing
Test Case 1: Scraping Reviews
Description: Test the scraper microservice to ensure it accurately scrapes reviews from an Amazon product page.

Input: A valid Amazon product URL.

Expected Output: A list of reviews (including reviewer name, rating, and review text).

Insert screenshot here for Test Case 1 output.

Test Case 2: Fake Review Classification
Description: Test the review-classifier microservice to check the accuracy of fake review detection.

Input: A set of example reviews (both fake and original).

Expected Output: A classification of each review as either "Fake" or "Original".

Insert screenshot here for Test Case 2 output.

Test Case 3: Review Relevance Scoring
Description: Test the relevance-scorer microservice to evaluate review relevance to the product.

Input: Product feature bullets and review text.

Expected Output: A relevance score indicating how related the review is to the product.

Insert screenshot here for Test Case 3 output.

☸️ Kubernetes Deployment (Alternative)
For Kubernetes/Minikube deployment:

Ensure Minikube is running:

bash
Copy code
minikube start
Navigate to the k8s folder:

bash
Copy code
cd k8s
Run the deployment script:

Windows:

bash
Copy code
run_fraudbuster(win).bat
Mac/Linux:

bash
Copy code
chmod +x run_fraudbuster(mac).sh
./run_fraudbuster(mac).sh
Check pod status:

bash
Copy code
kubectl get pods -w
Wait until all pods show STATUS: Running

Access the service:

bash
Copy code
minikube service flask-app-service
📊 Service Ports
Service	Port	Protocol
flask-app	5000	HTTP
review-classifier	50051	gRPC
relevance-scorer	50052	gRPC
scraper	50053	gRPC
mongo-store	50054	gRPC
redis	6379	TCP
mongo	27017	TCP

🐛 Troubleshooting
Port conflicts:
Check if ports are in use

bash
Copy code
netstat -an | findstr "5000"
Stop conflicting services or modify docker-compose.yml ports

Services not starting:
Check service logs

bash
Copy code
docker-compose logs <service-name>
Increase Docker memory allocation in Docker Desktop Settings

Old cached images:

bash
Copy code
docker-compose down
docker rmi -f caffeinatedkong/<service-name>:latest
docker-compose pull
docker-compose up -d
📝 Project Information
Course: CSC3104 - Cloud and Distributed Computing
Institution: Singapore Institute of Technology
Submission Date: November 16, 2025

👥 Contributors
Group 09 - FraudBuster Team

📄 License
This project is submitted as part of academic coursework.

For detailed testing instructions and submission requirements, please refer to GROUP09_INSTRUCTIONS.pdf.

vbnet
Copy code

### How to Add Images in Markdown:

You can insert images into your README by using the following syntax:

```markdown
![Alt text](path_to_image)
For local images: If your images are stored locally in a folder, like /assets/images/, use:

markdown
Copy code
![Scraper Output](assets/images/scraper_output.png)
For images hosted online: If the image is hosted online, use the full URL:

markdown
Copy code
![App Screenshot](https://link_to_image.com/screenshot.png)
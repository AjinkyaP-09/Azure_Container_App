# Automated CI/CD Pipeline to Azure Container Apps
This project demonstrates a complete, professional-grade CI/CD pipeline that builds, tests, scans, and deploys a Dockerized Python Flask application to a serverless environment in the Microsoft Azure cloud.

The entire process is orchestrated using GitHub Actions, triggering automatically on every push to the `main` branch.

### *Live Demo*

You can view the live, deployed application here:

https://app-cicd-project-8599.gentlerock-3b65b65c.eastus.azurecontainerapps.io/

<img width="1536" height="352" alt="image" src="https://github.com/user-attachments/assets/4918a782-ecf8-42e3-8112-2c6a7767b5f9" />


## Technologies Used:
1. Application: Python (Flask)

2. Containerization: Docker

3. CI/CD: GitHub Actions

4. Cloud Platform: Microsoft Azure

5. Container Registry: Azure Container Registry (ACR)

6. Hosting: Azure Container Apps (Serverless Containers)

<img width="1919" height="589" alt="image" src="https://github.com/user-attachments/assets/8e2236f1-caea-4ad0-beb8-702587982ae2" />


## Pipeline Workflow
The CI/CD pipeline is defined in `.github/workflows/main.yml` and is split into two dependent jobs:

### Job 1: Build & Scan
**1. Trigger:** The workflow is automatically triggered by a `git push` to the `main` branch of this repository.

**2. Checkout Code:** The job begins by checking out the latest version of the source code.

**3. Azure Authentication:** The workflow securely authenticates with Azure using a Service Principal credential stored as a GitHub Secret.

**4. Build and Push Docker Image:**

 - The workflow builds a Docker image from the `Dockerfile`.

 - It tags the image with the unique Git commit SHA for versioning.

 - It then logs into Azure Container Registry (ACR) and pushes the newly built image.

**5. Deploy to Azure Container Apps:**

 - The final step deploys the application by creating or updating an Azure Container App.

 - It creates a new revision with the new container image, ensuring a zero-downtime deployment.

 - The action securely passes the ACR credentials to the Container App, granting it permission to pull the private image.

<img width="1898" height="1070" alt="image" src="https://github.com/user-attachments/assets/b557059a-1621-44fa-9a36-fbd2a4339b3e" />

## Project Structure
```
.
├── .github/
│   └── workflows/
│       └── main.yml      # <-- Defines the advanced CI/CD pipeline
├── app.py                # <-- Python Flask application
├── Dockerfile            # <-- Instructions to build the Docker image
├── requirements.txt      # <-- Python dependencies (including flake8)
└── README.md
```

## Configuration & Security
**`AZURE_CREDENTIALS`:** A JSON object containing the Service Principal credentials for authenticating with Azure.

**`ACR_USERNAME / ACR_PASSWORD`:** Admin credentials for the Azure Container Registry, used to grant the Container App pull permissions.

All credentials are stored as encrypted secrets in the GitHub repository settings and are not exposed in the workflow logs.

# End-to-End Deep Learning Project: AWS CI/CD Deployment with GitHub Actions

## Overview

This repository demonstrates an end-to-end deep learning workflow, including deployment on AWS using GitHub Actions for continuous integration and continuous deployment (CI/CD). Below are the steps and instructions to replicate this setup.

## Workflows

1. **Update Configuration Files:**
   - Modify `config.yaml` for general settings.
   - (Optional) Adjust `secrets.yaml` for secure parameters.
   - Update `params.yaml` for model parameters.

2. **Project Structure Updates:**
   - Update entities as needed.
   - Modify the configuration manager in the `src/config` directory.
   - Update components related to the pipeline.
   - Modify `main.py` as necessary.
   - Update `dvc.yaml` for data version control.

3. **Final Deployment Steps:**
   - Ensure `app.py` is updated for deployment.

## How to Run?

### Steps:

1. **Clone the Repository:**

   ```bash
   git clone https://github.com/MinhTienTH/End-to-End-Deep-Learning-Project-AWS-CICD-Deployment-with-Github-Actions.git
   ```
2. **Create a Conda Environment:**

&nbsp;&nbsp;&nbsp;&nbsp;After opening the repository, create and activate a new Conda environment:

```bash
conda create -n cnncls python=3.8 -y
conda activate cnncls
```

3. **Install Requirements:**

&nbsp;&nbsp;&nbsp;&nbsp;Install the necessary packages:

```bash
pip install -r requirements.txt
```

4. **Run the Application:**

&nbsp;&nbsp;&nbsp;&nbsp;Execute the application:

```bash
python app.py
```

5. **Access the Application:**

&nbsp;&nbsp;&nbsp;&nbsp;Open your local host and port to access the application.

## MLflow Integration
MLflow is integrated into this project for tracking experiments and models.
   - MLflow Documentation
   - MLflow Tutorial

**MLflow Commands:**
   - Start the MLflow UI:

```bash
mlflow ui
```

**Integration:**
You can use Dagshub for remote MLflow tracking:

```bash
export MLFLOW_TRACKING_URI=https://dagshub.com/entbappy/Kidney-Disease-Classification-MLflow-DVC.mlflow
export MLFLOW_TRACKING_USERNAME=entbappy
export MLFLOW_TRACKING_PASSWORD=6824692c47a369aa6f9eac5b10041d5c8edbcef0
```

## DVC Commands
**1. Initialize DVC:**

```bash
dvc init
```

**2. Reproduce the Pipeline:**

```bash
dvc repro
```

**3. Visualize the Pipeline:**

```bash
dvc dag
```

## About MLflow & DVC
**MLflow:**
   - Production-grade experiment tracking.
   - Facilitates logging and tagging models.
     
**DVC:**
   - Lightweight experiment tracking for proof of concept (POC).
   - Supports orchestration and pipeline creation.

## AWS CI/CD Deployment with GitHub Actions

**1. Login to AWS Console.**<p>
**2. Create an IAM User for Deployment:**

   - Provide specific access:
         <p>&nbsp;&nbsp;&nbsp;&nbsp;2.1.1. EC2 access for virtual machines.
         <p>&nbsp;&nbsp;&nbsp;&nbsp;2.1.2. ECR (Elastic Container Registry) for storing Docker images.

   - Deployment Overview:
         <p>&nbsp;&nbsp;&nbsp;&nbsp;2.2.1. Build a Docker image of the source code.
         <p>&nbsp;&nbsp;&nbsp;&nbsp;2.2.2. Push the Docker image to ECR.
         <p>&nbsp;&nbsp;&nbsp;&nbsp;2.2.3. Launch an EC2 instance.
         <p>&nbsp;&nbsp;&nbsp;&nbsp;2.2.4. Pull the Docker image from ECR to EC2.
         <p>&nbsp;&nbsp;&nbsp;&nbsp;2.2.5. Run the Docker container on EC2.

   - Policies:
         <p>&nbsp;&nbsp;&nbsp;&nbsp;2.3.1. 'AmazonEC2ContainerRegistryFullAccess'
         <p>&nbsp;&nbsp;&nbsp;&nbsp;2.3.2. 'AmazonEC2FullAccess'

**3. Create an ECR Repository:**

   - Save the URI, e.g., **'566373416292.dkr.ecr.us-east-1.amazonaws.com/chicken'**

**4. Create an EC2 Machine (Ubuntu).**

**5. Install Docker on the EC2 Machine:**

```bash
sudo apt-get update -y
sudo apt-get upgrade
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker ubuntu
newgrp docker
```

**6. Configure EC2 as a Self-Hosted Runner:**

   - Navigate to Settings > Actions > Runner > New self-hosted runner.
   - Choose the OS and follow the instructions to run the commands.

**7. Set Up GitHub Secrets:**

Add the following secrets in your GitHub repository:
   - AWS_ACCESS_KEY_ID
   - AWS_SECRET_ACCESS_KEY
   - AWS_REGION (e.g., us-east-1)
   - AWS_ECR_LOGIN_URI (e.g., 566373416292.dkr.ecr.ap-south-1.amazonaws.com)
   - ECR_REPOSITORY_NAME (e.g., simple-app)

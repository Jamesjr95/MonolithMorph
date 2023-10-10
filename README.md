## Project Name 

MonolithMorph

## Description

In this project, I successfully deployed a monolithic Node.js application to a Docker container and then decoupled it into microservices without any downtime. The application I built is a message board that allows users to interact through threads and messages.

## Prerequisites

1. **AWS Account**: [Sign up here](https://aws.amazon.com/) if you don't have one.
2. **Docker**: Install for [Mac](https://docs.docker.com/docker-for-mac/install/) or [Windows](https://docs.docker.com/docker-for-windows/install/). 
   - Confirm installation with:
     ```bash
     docker --version
     ```

3. **AWS CLI**: 
    - [Getting Started with AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html).
    - Confirm installation:
      ```bash
      aws --version
      ```

4. **AWS Copilot**: On macOS, install using brew:
    ```bash
    brew install aws/tap/copilot-cli
    ```

## Deployment Steps

### 1. Initialize AWS Copilot Application
    ```bash
    cd ./amazon-ecs-nodejs-microservices/
    copilot app init
    ```

### 2. Set Up Environment
    ```bash
    copilot env init
    ```

### 3. Deploy the Environment
    ```bash
    copilot env deploy --name api
    ```

### 4. Set Up Monolithic AWS Copilot Service
    ```bash
    copilot svc init
    ```

### 5. Deploy the Monolithic Service
    ```bash
    copilot svc deploy --name monolith
    ```

### 6. Test the Deployment
Use the provided AWS Copilot URL to test endpoints.

## Creating Microservices

### 1. Initialize the Microservices
    ```bash
    copilot svc init --app api --dockerfile ./3-microservices/services/posts/Dockerfile --name posts --svc-type "Load Balanced Web Service"
    copilot svc init --app api --dockerfile ./3-microservices/services/threads/Dockerfile --name threads --svc-type "Load Balanced Web Service"
    copilot svc init --app api --dockerfile ./3-microservices/services/users/Dockerfile --name users --svc-type "Load Balanced Web Service"
    ```

### 2. Configure Service Paths
AWS Copilot sets the path based on the service name. Edit the `manifest.yml` for each service to adjust the path.

## Deploying Microservices

### 1. Deploy the Microservices
    ```bash
    copilot svc deploy --name posts
    copilot svc deploy --name threads
    copilot svc deploy --name users
    ```

### 2. Shut down the Monolith
    ```bash
    copilot svc delete --name monolith
    ```

### 3. Verify the Deployment
Use the provided URLs to validate the microservices deployment.

## Cleanup and Conclusion

### 1. Delete the Application
    ```bash
    copilot app delete --name api
    ```

Congratulations! You've now broken a monolithic application into microservices, offering more flexibility and scalability.

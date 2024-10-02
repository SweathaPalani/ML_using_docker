Project Name: ML_using_docker

## Overview

This project involves setting up a machine learning (ML) endpoint in a Docker container. The project demonstrates how to build a Docker container with a deployed ML model, and includes instructions on how to test the ML endpoint after the container is running.

Key features:
- **Dockerized ML Model**: The project uses Docker to containerize the environment required to run the ML model.
- **REST API for Model Serving**: The ML model is accessible through a REST API, allowing for easy interaction and testing.
- **Simple Testing Endpoint**: The API provides an endpoint to send test data and receive predictions in real-time.

## Prerequisites

Ensure the following dependencies are installed on your system before proceeding:
- **Docker**: Version 20.10 or above
- **Docker Compose** (optional): Version 1.28 or above
- **curl**: For testing the endpoint

## Instructions to Build and Run the Docker Container

1. **Clone the Repository**:
   Clone the project repository to your local machine.
   ```bash
   git clone https://github.com/SweathaPalani/ML_using_docker.git
   cd ML_using_docker
   ```

2. **Build the Docker Image**:
   Use the following command to build the Docker image. The `Dockerfile` located in the root directory will be used to create the image.
   ```bash
   docker build -t ml-model-api .
   ```

3. **Run the Docker Container**:
   After building the image, run the container using the command below. The container will start a server (e.g., Flask/FastAPI) exposing the ML model via a REST API.
   ```bash
   docker run -p 5000:5000 ml-model-api
   ```
   This will map the container's port `5000` to your local machine's port `5000`.

4. **Check Docker Container Status**:
   You can check if the container is running by listing active Docker containers:
   ```bash
   docker ps
   ```

## Instructions to Test the ML Endpoint

Once the Docker container is up and running, you can test the ML endpoint by sending a request to it.

1. **Test the Health Check**:
   To ensure the server is running, send a GET request to the health check endpoint:
   ```bash
   curl http://localhost:5000/health
   ``

2. **Test the ML Model Prediction**:
   Send a POST request to the prediction endpoint with some test data (modify the JSON input as per your model):
   ```bash
   curl -X POST http://localhost:5000/predict -H "Content-Type: application/json" -d '{"input_data": [data]}'
   ```
   Example:
   ```bash
   curl -X POST http://localhost:5000/predict -H "Content-Type: application/json" -d '{"input_data": [5.1, 3.5, 1.4, 0.2]}'
   ```
   The response should include a prediction like:
   ```json
   {"prediction": "Iris-setosa"}
   ```

## Troubleshooting

If you encounter issues while building or running the Docker container, try the following:

- Ensure Docker is installed and running correctly by checking its status:
  ```bash
  docker --version
  ```
- Check the container logs for any errors:
  ```bash
  docker logs <container_id>
  ```

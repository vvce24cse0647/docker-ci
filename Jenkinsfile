pipeline {
    agent any

    environment {
        REGISTRY = "localhost:5000"
        IMAGE_NAME = "anil-demo-app"
    }

    stages {
        stage('1. Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('2. Application Build & Test') {
            steps {
                bat 'C:\\Users\\STUDENT\\AppData\\Local\\Programs\\Python\\Python313\\python.exe -m py_compile app.py'
            }
        }

        stage('3. Build & Tag Docker Image') {
            steps {
                bat "C:\\Users\\STUDENT\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe build -t ${REGISTRY}/${IMAGE_NAME}:${BUILD_NUMBER} -t ${REGISTRY}/${IMAGE_NAME}:latest ."
            }
        }

        stage('4. Push Image to Registry') {
            steps {
                bat "C:\\Users\\STUDENT\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe push ${REGISTRY}/${IMAGE_NAME}:${BUILD_NUMBER}"
                bat "C:\\Users\\STUDENT\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe push ${REGISTRY}/${IMAGE_NAME}:latest"
            }
        }
    }

    post {
        success {
            echo "Pipeline succeeded! Image ${REGISTRY}/${IMAGE_NAME}:${BUILD_NUMBER} is available locally and in the registry."
        }
    }
}

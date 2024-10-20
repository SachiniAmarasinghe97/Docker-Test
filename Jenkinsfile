pipeline {
    agent any

    tools { 
        nodejs 'NodeJS_Installation'
    }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', 
                    url: 'https://github.com/SachiniAmarasinghe97/Sample-app-cicd.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install npm dependencies
                bat 'npm install' 
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build the Docker image
                bat 'docker build -t sachini2524/node:latest .'
            }
        }

        stage('Run Docker Container') {
            steps {
                // Run the Docker container with the newly built image
                bat 'docker run -d -p 3000:3000 --name node_app sachini2524/node:latest'
            }
        }
    }

    post {
        always {
            // Cleanup actions, such as stopping and removing the Docker container
            bat 'docker stop node_app || true'  // Ensure it doesn’t fail if not running
            bat 'docker rm node_app || true'
        }
    }
}
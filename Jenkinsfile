pipeline {
    agent any

    environment {
        REPO_URL = "https://github.com/yugen-21/task-7.git"
        IMAGE_NAME = "flask_app"
        CONTAINER_NAME = "flask_container"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: "${REPO_URL}"
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t %IMAGE_NAME% ."
            }
        }

        stage('Run Docker Container') {
            steps {
                bat """
                docker run -d -p 5000:5000 --name %CONTAINER_NAME% %IMAGE_NAME%
                """
            }
        }

        stage('Cleanup Old Docker Images') {
            steps {
                bat "docker rmi -f %IMAGE_NAME% 2>nul"
            }
        }
    }

    post {
        always {
            echo "Pipeline Execution Completed!"
        }
    }
}

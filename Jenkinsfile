pipeline {
    agent any

    environment {
        IMAGE_NAME = "python-docker-app"
        CONTAINER_NAME = "python-app"
        PORT = "5000"
    }

    stages {

        stage("Clone Repo") {
            steps {
                git branch: 'main',
                    url: 'https://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@github.com/thakurrajesh22293/newprojectpython.git'
            }
        }

        stage("Build Docker Image") {
            steps {
                sh """
                docker build -t $IMAGE_NAME:latest .
                """
            }
        }

        stage("Stop Old Container") {
            steps {
                sh """
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                """
            }
        }

        stage("Run Container") {
            steps {
                sh """
                docker run -d \
                  --name $CONTAINER_NAME \
                  -p $PORT:$PORT \
                  $IMAGE_NAME:latest
                """
            }
        }
    }

    post {
        success {
            echo "✅ Deployment completed successfully"
        }
    }
}

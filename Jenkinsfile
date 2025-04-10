pipeline {
    agent any
     environment {
        IMAGE_NAME = 'studysync-docker-app'
        CONTAINER_NAME = 'studysync-container'
        PORT = '8000'
    }
   

    stages {
        stage('git clone') {
            steps {
                echo 'clone code from github'
                git branch: 'main', url: 'https://github.com/Soumil2002/StudySync.git'
            }
        }
        stage('Build Docker image') {
            steps {
                echo 'Building Docker image'
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        stage('Stop & Remove Existing Container') {
            steps {
                echo 'Stopping and removing old container if it exists...'
                sh '''
                    if [ "$(docker ps -aq -f name=$CONTAINER_NAME)" ]; then
                        docker stop $CONTAINER_NAME || true
                        docker rm $CONTAINER_NAME || true
                    fi
                '''
            }
        }
        stage('Run Docker image') {
            steps {
                echo 'Running Docker container...'
                sh 'docker run -d -p $PORT:80 --name $CONTAINER_NAME $IMAGE_NAME'
            }
        }
    }
}

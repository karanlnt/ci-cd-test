pipeline {
    agent any

    environment {
        IMAGE_NAME = "ci-cd-test"
        CONTAINER_NAME = "ci-cd-test"
        APP_DIR = "ci-cd-test"
        GIT_REPO = "https://github.com/AdminVelesium/ci-cd-test"
    }

    stages {
        stage('Prepare Directory') {
            steps {
                sh '''
                    rm -rf $APP_DIR
                    mkdir -p $APP_DIR
                '''
            }
        }

        stage('Clone Repository') {
            steps {
                dir("$APP_DIR") {
                    git branch: 'main', credentialsId: 'e90f8a68-032a-495b-8049-16a9162f072e', url: 'https://github.com/karanlnt/ci-cd-test.git'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                dir("$APP_DIR") {
                    sh 'docker build -t $IMAGE_NAME .'
                }
            }
        }

        stage('Stop & Remove Existing Container') {
            steps {
                sh '''
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 5000:5000 --name $CONTAINER_NAME $IMAGE_NAME'
            }
        }
    }
}

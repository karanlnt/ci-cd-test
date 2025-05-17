pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                echo 'Cloning repo...'
                checkout scm
            }
        }

        stage('Set Up Python') {
            steps {
                sh '''
                    sudo apt install python3.12-venv
                    sudo apt update
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install flask
                '''
            }
        }

        stage('Run Flask App') {
            steps {
                sh '''
                    export JENKINS_NODE_COOKIE=dontKillMe
                    . venv/bin/activate
                    nohup python3 app.py > app.log 2>&1 &
                '''
            }
        }
    }
}

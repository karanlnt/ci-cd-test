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
                script {
                    // Ensure Python 3 and pip are installed
                    sh '''
                        sudo apt update
                        sudo apt install -y python3 python3-pip python3-venv
                        python3 -m venv venv
                        . venv/bin/activate
                        pip install flask
                    '''
                }
            }
        }

        stage('Run Flask App') {
            steps {
                script {
                    // Ensure the Flask app runs as a background process
                    sh '''
                        export JENKINS_NODE_COOKIE=dontKillMe
                        . venv/bin/activate
                        nohup python3 app.py > app.log 2>&1 &
                    '''
                }
            }
        }
    }
}

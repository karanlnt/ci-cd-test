pipeline {
    agent any
    
    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        
        stage('Clone Repo') {
            steps {
                echo "Cloning repo..."
            }
        }
        
        stage('Set Up Python') {
            steps {
                script {
                    // Install the python3-venv package if not present
                    sh 'sudo apt-get update'
                    sh 'sudo apt-get install -y python3.12-venv'
                    
                    // Now try to create the virtual environment
                    sh 'python3 -m venv venv'
                }
            }
        }
        
        stage('Run Flask App') {
            steps {
                echo "Running Flask app..."
                // Add your commands to run the Flask app here
            }
        }
    }
}

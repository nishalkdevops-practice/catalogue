pipeline {
    agent { node { label 'AGENT-1' } }
    options {
        timeout(time: 1, unit: 'HOURS')
    }
    stages {
        
        stage('Install dependencies') {
            steps {
                sh 'sudo npm install'
            }
        }

        stage('Unit Test') {
            steps {
                echo "unit testing is done here"
            }
        }

        stage('Sonar scan') {
           steps {
                 sh 'sonar-scanner'
                echo "unit testing is done here...."
            }
        }

        stage('Deployment') {
           steps {
                 
                echo "Deployment is done...."
            }
        }
    }

    
    
}
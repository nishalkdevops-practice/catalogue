pipeline {
    agent { node { label 'Agent-1' } }
    stages {
        
        stage('Install dependencies') {
            steps {
                sh 'sudo npm install'
            }
        }

        stage('Unit Test') {
            steps {
                echo "unit testing is done here...."
            }
        }

        stage('Sonar scan') {
            steps {
                sh 'sonar-scanner'
                echo "unit testing is done here...."
            }
        }
    }

    
    
}
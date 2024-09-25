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

        stage('Build') {
            steps {

                sh 'ls -lrt'
                sh 'zip -r  ./* --exclude=.git --exclude=.zip'
            
            }
        }

          //install pipeline utility steps plugin, if not installed



        stage('Publish artifact') {
            steps {

                sh 'ls -lrt'
                sh 'zip -r  catalogue.zip ./* --exclude=.git --exclude=.zip'
            
            }
        }

        stage('Publish Artifact') {
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: '54.204.155.165:8081/',
                    groupId: 'com.roboshop',
                    version: '1.0.1',
                    repository: 'catalogue',
                    credentialsId: 'nexus-auth',
                    artifacts: [
                        [artifactId: 'catalogue',
                        classifier: '',
                        file: 'catalogue.zip',
                        type: 'zip']
                    ]
                )
            }
        }


        stage('Deployment') {
           steps {
                 
                echo "Deployment is done...."
            }
        }


    }

    post{
        always{
            echo 'cleaning up workspace'
            deleteDir()
        }
    }
}

    
    

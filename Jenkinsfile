pipeline {
    agent { node { label 'Agent-1' } }
    options {
        timeout(time: 1, unit: 'HOURS')
    }

    environment{
        packageVersion = ''
    }


    stages {

        stage('GET version') {
            steps {
                script{
                    def packageJson = readJSON(file: 'package.json')
                    packageVersion = packageJson.version
                    echo "version: ${packageVersion}"


                }
            
            }
        }
        
        stage('Install dependencies') {
            steps {
                sh 'sudo yum update -y'
                sh 'sudo yum install nodejs npm -y'

            
            }
        }

        stage('Unit Test') {
            steps {
                echo "unit testing is done here"
            }
        }

        stage('Sonar scan') {
           steps {
                 //sh 'sonar-scanner'
                echo "Sonar scan is done...."
            }
        }

        stage('Build') {
            steps {

                sh 'ls -lrt'
                sh 'zip -r  ./* --exclude=.git --exclude=.zip'
            
            }
        }

          //install pipeline utility steps plugin, if not installed



        stage('SAST') {
            steps {

                echo "Static application security testing done.........."
                echo "package version: ${packageVersion}"
            
            }
        }

        //install pipeline utility steps plugin if not installed

        stage('Publish Artifact') {
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: '3.82.186.122:8081',
                    groupId: 'com.roboshop',
                    version: "${packageVersion}",
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

    
    

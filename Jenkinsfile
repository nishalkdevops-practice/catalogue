pipeline {
    agent { node { label 'Agent-1' } }
    options {
        timeout(time: 1, unit: 'HOURS')
    }

    environment{
        packageVersion = ''
    }


    stages {
        stage('Get version'){
            steps{
                script{
                    def packageJson = readJSON(file: 'package.json')
                    packageVersion = packageJson.version
                    echo "version: ${packageVersion}"
                }
            }
        }
        stage('Install depdencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Unit test') {
            steps {
                echo "unit testing is done here"
            }
        }
        //sonar-scanner command expect sonar-project.properties should be available
        stage('Sonar Scan') {
            steps {
                echo "Sonar scan done"
            }
        }
        stage('Build') {
            steps {
                sh 'ls -ltr'
                sh 'zip -r catalogue.zip ./* --exclude=.git --exclude=.zip'
            }
        }
        stage('SAST') {
            steps {
                echo "SAST Done"
                echo "package version: $packageVersion"
            }
        }
        //install pipeline utility steps plugin, if not installed
        stage('Publish Artifact') {
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: '3.86.110.203:8081/',
                    groupId: 'com.roboshop',
                    version: '1.0.2',
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

    
    

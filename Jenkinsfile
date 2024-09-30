pipeline {
    agent { node { label 'Agent-1' } }
    options {
        timeout(time: 1, unit: 'HOURS')
    }
    stages {

        stage('GET version') {
            steps {
                script{
                    def packageJson = readJson file: 'package.json'
                    def packageversion = packageJSON.Version
                    echo "${packageJSONVersion}"


                }
            
            }
        }
        
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
            
            }
        }

        //install pipeline utility steps plugin if not installed

        // stage('Publish Artifact') {
        //     steps {
        //         nexusArtifactUploader(
        //             nexusVersion: 'nexus3',
        //             protocol: 'http',
        //             nexusUrl: '172.31.89.51:8081/',
        //             groupId: 'com.roboshop',
        //             version: '1.0.3',
        //             repository: 'catalogue',
        //             credentialsId: 'nexus-auth',
        //             artifacts: [
        //                 [artifactId: 'catalogue',
        //                 classifier: '',
        //                 file: 'catalogue.zip',
        //                 type: 'zip']
        //             ]
        //         )
        //     }
        // }


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

    
    

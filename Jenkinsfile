pipeline {

    agent any

    stages {

        stage ('Git checkout') {

            steps {

                git branch: 'main', url: 'https://github.com/sekharpa/demo-counter-app.git'
            }
        }

        stage ('UNIT Testing ') {

            steps {

                sh 'mvn clean test'
            }
        }

        stage ('Integration Testing ') {

            steps {

                sh 'mvn verify -DskipUnitTests'
            }
        }
    
        stage ('Maven Build ') {

            steps {

                sh 'mvn clean install'
            }
        }

        stage ('Sonarqube analaysis') {

            steps {

                script {

                      withSonarQubeEnv (abortPipeline: false, credentialsId: 'newsonartoken') {

                            sh 'mvn clean package sonar:sonar'
                      }
                         

                }

            }

        }    

       
           stage ('Quality gate status') {

            steps {

            script {

                waitForQualityGate abortPipeline: false, credentialsId: 'newsonartoken'
            }
         } 
    }  

            stage ('uplaod jar to nexus') {

                steps {

                    script {

                        nexusArtifactUploader artifacts: [[artifactId: 'springboot', classifier: '', file: 'target/Uber.jar', type: 'jar']], 
                        credentialsId: 'nexusauth', 
                        groupId: 'com.example', 
                        nexusUrl: '13.211.161.7:8081', 
                        nexusVersion: 'nexus3', 
                        protocol: 'http', 
                        repository: 'http://13.211.161.7:8081/repository/demoapp-release/', 
                        version: '1.0.0'
                    }
                }
            }
       
    }

}

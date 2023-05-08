pipeline {

    agent any

    stages {

        stage ('Git checkout') {

            steps {

                git branch: 'main', url: 'https://github.com/sekharpa/demo-counter-app.git'
            }
        }

	 stage ('UNIT testing') {

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
 	
           stage('Static code  analaysis') {

            steps {

              script{
 
		withSonarQubeEnv (abortPipeline: false, credentialsId: 'sonarqubeapikey') {
                sh 'mvn clean package sonar:sonar'

		}
            }
	}		

    }	   	

	stage ('upload jar file to nexus'){

	steps {

	   script {

		nexusArtifactUploader artifacts: [[artifactId: 'springboot', classifier: '', file: 'target/Uber.jar', type: 'jar']], credentialsId: 'nexusauth', groupId: 'com.example', nexusUrl: '3.27.44.65:8081', nexusVersion: 'nexus3', protocol: 'https', repository: 'maven-releases', version: '1.0.0'
          
            }
          }

	}	 

    }

 }	

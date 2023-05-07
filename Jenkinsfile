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
 	
           stage ('Static ,code ananlysis ') {

            steps {

              script{  waitForQualityGate abortPipeline: false, credentialsId: 'sonarqubeapikey'
                sh 'mvn clean package sonar:sonar'
            }
	}		
        }	


  }

}

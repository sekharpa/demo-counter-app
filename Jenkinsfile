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

  }

}

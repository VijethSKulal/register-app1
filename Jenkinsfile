pipeline {
    agent { label'Jenkins-Agent'}
    tools {
        jdk 'Java17'
        maven 'Maven3'  // Change 'Maven3' to 'maven3'
    }
    stages {
        stage("Cleanup Workspace") {
            steps {
                cleanWs()
            }
        }

        stage("Checkout from SCM") {
            steps {
                git branch: 'main', credentialsId: 'Github', url: 'https://github.com/VijethSKulal/register-app1.git'
            }
        }

        stage("Build Application") {
            steps {
                sh "mvn clean package"
            }
        }

        stage("Test Application") {
            steps {
                sh "mvn test"
            }
        }
     stage("SonarQube Analysis"){
           steps {
	           script {
		           withSonarQubeEnv(credentialsId:'jenkins-sonarqube-token') {
                       sh "mvn sonar:sonar"
		               }
	            }	
            }
     }

    }
}

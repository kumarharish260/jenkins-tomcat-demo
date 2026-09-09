/*
This is the code of jenkins groovy deploy the project automatically without using the docker file. 
pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build WAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Verify WAR') {
            steps {
		sh 'ls -lh target/*.war'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [
                    tomcat9(
                        credentialsId: 'tomcat-prod-credentials',
                        url: 'http://172.30.205.31:8080'
                    )
                ],
                contextPath: 'jenkins-tomcat-demo',
                war: 'target/*.war'
            }
        }
    }

    post {
        success {
            echo 'WAR deployment completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}
*/



// This is the code of jenkins groovy deploy the project automatically without using the docker file.//
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Verify WAR') {
            steps {
                sh 'ls -lh target/jenkins-tomcat-demo.war'
            }
        }

        stage('Docker Build') {
            steps {
                sh '''
                    docker build \
                    -t jenkins-tomcat-demo:latest .
                '''
            }
        }

        stage('Docker Image Verify') {
            steps {
                sh 'docker images | grep jenkins-tomcat-demo'
            }
        }
    }

    post {
        success {
            echo 'Maven build and Docker image creation completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}

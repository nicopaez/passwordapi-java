pipeline {

    triggers {
        pollSCM('H/5 * * * *')
    }

    agent any

    stages {
        stage('checkout') {
            steps {
                checkout scm
            }
        }

        stage('compile and test') {
            agent {
               docker {
                   image 'maven:3.5.0-jdk-8-slim'
                   args '-v /root/.m2:/root/.m2'
                }
            }
            steps {
                sh 'mvn clean package'
            }
        }

        stage('image') {
            steps {
                sh "docker build -t nicopaez/passwordapi-java:taller . --build-arg JAR_FILE=./target/passwordapi-1.5.1.jar"
            }
        }
        stage('publish') {
            steps {
                sh "docker push nicopaez/passwordapi-java:taller"
            }
        }
        stage('deploy') {
            steps {
                echo 'running kubectl'
            }
        }
        stage('acceptance_test') {
            steps {
                echo 'testing'
            }
        }        
    }
}


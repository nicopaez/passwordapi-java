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

        stage('test') {
            agent {
               docker {
                   image 'maven:3.5.0-jdk-8-slim'
                }
            }
            steps {
                sh 'mvn clean test'
            }
        }

        stage('package') {
            steps {
                echo '.'
            }
        }
        stage('publish') {
            steps {
                echo '.'
            }
        }
        stage('deploy') {
            steps {
                echo '.'
            }
        }
        stage('acceptance_test') {
            steps {
                echo '.'
            }
        }        
    }
}


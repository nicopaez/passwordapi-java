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
                stash includes: 'target/*jar', name: 'binaries'
            }
        }

        stage('image') {
            steps {
                unstash 'binaries'
                sh "docker build -t nicopaez/passwordapi-java:taller\${BUILD_ID} . --build-arg JAR_FILE=./target/passwordapi-1.5.2.jar"
            }
        }
        stage('publish') {
            steps {
                sh "docker push nicopaez/passwordapi-java:taller\${BUILD_ID}"
            }
        }
        stage('deploy') {
            steps {
                echo "kubectl set image deployment/passnico passnico=nicopaez/passwordapi-java:taller\${BUILD_ID}"
            }
        }
        stage('acceptance_test') {
            steps {
                echo 'curl http://178.128.128.101/actuator/health'
            }
        }        
    }
}


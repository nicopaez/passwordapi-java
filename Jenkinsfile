pipeline {
    options {
        buildDiscarder(logRotator(numToKeepStr: '20'))
        disableConcurrentBuilds()
    }

    triggers {
        cron('H H(9-18)/4 * * 1-5')
        pollSCM('H/5 * * * *')
    }

    agent {
        docker {
            image 'maven:3.6.1-jdk-8-slim'
        }
    }
    
    stages {

        stage('Clone repo') {
            steps{
                checkout([$class: 'GitSCM', branches: [[name: 'refs/heads/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CleanBeforeCheckout']], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/nicopaez/passwordapi-java.git']]])
            }
        }

        stage('build') {

            steps {
                sh "cd . && mvn clean test"
            }
        }

        stage('package') {
            steps {
                sh "docker build --tag passwordapijava:latest --file Dockerfile-java8 ."
            }
        }

    }
    post {
        always {
            sh 'echo "the END"'
        }
    }
}
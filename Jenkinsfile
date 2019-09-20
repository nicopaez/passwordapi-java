pipeline {
    options {
        buildDiscarder(logRotator(numToKeepStr: '20'))
        disableConcurrentBuilds()
    }

    triggers {
        cron('H H(9-18)/4 * * 1-5')
        pollSCM('H/5 * * * *')
    }

    agent any
    
    stages {
        stage('Clone repo') {
            steps{
                checkout([$class: 'GitSCM', branches: [[name: 'refs/heads/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CleanBeforeCheckout']], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/nicopaez/passwordapi-java.git']]])
            }
        }

        stage('build') {
            steps {
                sh "mvn clean test"
            }
        }

        stage('package') {
            steps {
                sh "mvn clean package -DskipTests"
                sh """
                    JAR_FILE=`ls target/*.jar | sed 's/target\\///'`
                    VERSION=`echo \${JAR_FILE} | sed 's/passwordapi-//' | sed 's/.jar//'`
                    docker build --tag passwordapi-java:\${VERSION} --build-arg JAR_FILE=target/passwordapi-\${VERSION}.jar --file Dockerfile .
                    """
            }
        }
    }
    post {
        always {
            sh 'echo "the END"'
        }
    }
}
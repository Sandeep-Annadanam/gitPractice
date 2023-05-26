pipeline {
    agent any
    parameters {
        choice(name: 'VERSION', choices: ['1.1.1','2.2.2','3.3.3'], description: '')
        booleanParam(name: 'executeTest', defaultValue: true, description: '')
    }
    environment {
        NEW_VERSION = '1.3.6'
        SERVER_CREDENTIALS = credentials('server-cred')
    }
    stages {
        stage('GIT CLONE') {
            steps{
                git 'https://github.com/Akiranred/hello-world.git'
                echo "git clone completed"
            }
        }
        stage('CLEANING'){
            steps{
                sh 'mvn clean'
                echo "mvn clean completed"
            }
        }
        stage('TESTING') {
            when {
                expression{
                    params.executeTest
                }
            }
            steps{
                echo "**** TESTING*****"
                sh 'mvn test'
            }
        }
        stage('COMPILE'){
            steps{
                sh 'mvn compile'
                echo "mvn compile completed"
            }
        }
        stage('PACKAGE'){
            steps {
                echo "building the version ${params.VERSION}"
                sh 'mvn package'
                echo "mvn package completed"
            }
        }
    }
}


pipeline {
    agent any 
    environment {
        caminhoPacote = 'target/verademo.war'
        wrapperVersion = '23.8.12.0'
        appProfile = 'verademo-java-web'
    }
    stages {
        stage('Build MAVEN') { 
            steps {
                sh 'mvn clean package'
                sh 'ls -l target/'
            }
        }

        stage('Build IMMGE') { 
            steps {
                sh 'docker build -t verademo:"${BUILD_NUMBER}" .'
            }
        }
    }
}

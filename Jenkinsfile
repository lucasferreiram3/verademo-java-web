pipeline {
    agent any 
    environment {
        caminhoPacote = 'target/verademo.war'
        wrapperVersion = '23.8.12.0'
    }
    
    stages {
        stage('Build') { 
            steps {
                sh 'mvn clean package'
                sh 'ls -l target/'
            }
        }
    }
}
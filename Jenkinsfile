pipeline {
    agent any 
    environment {
        caminhoPacote = 'target/verademo.war'
        wrapperVersion = '23.8.12.0'
        appProfile = 'verademo-java-web'
    }
    stages {
        stage('Build Maven') { 
            steps {
                sh 'mvn clean package'
                sh 'ls -l target/'
            }
        }

        stage('Build Image') { 
            steps {
                sh 'docker build -t verademo:v"${BUILD_NUMBER}" .'
            }
        }

        stage('Aqua Image Scan') { 
            steps {
                withCredentials([string(credentialsId: 'AQUA_USER', variable: 'AQUA_USER'), string(credentialsId: 'AQUA_PASSWORD', variable: 'AQUA_PASS'), string(credentialsId: 'AQUA_HOST', variable: 'AQUA_HOST'), string(credentialsId: 'AQUA_SCANNER', variable: 'AQUA_SCANNER')]) {
                    sh 'docker login registry.aquasec.com -u ${AQUA_USER} -p ${AQUA_PASS}'
                    sh 'docker pull registry.aquasec.com/scanner:latest-saas'
                    sh 'docker run -v /var/run/docker.sock:/var/run/docker.sock registry.aquasec.com/scanner:latest-saas scan -H {AQUA_HOST} -A ${AQUA_SCANNER} --local verademo:v"${BUILD_NUMBER}"'
                }
            }
        }
    }
}

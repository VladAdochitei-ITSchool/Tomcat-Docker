pipeline {
agent any
   
tools {
    maven 'Maven3'
}

environment {
    IMAGE_NAME = 'tomcat-demo'
}

stages {

    stage('Checkout') {
        steps {
            git 'https://github.com/YOUR_USER/Tomcat-Docker.git'
        }
    }

    stage('Build WAR') {
        steps {
            sh 'mvn clean package'
        }
    }

    stage('Build Docker Image') {
        steps {
            sh 'docker build -t $IMAGE_NAME .'
        }
    }

    stage('Run Container') {
        steps {
            sh '''
            docker rm -f tomcat-demo || true
            docker run -d -p 8081:8080 --name tomcat-demo $IMAGE_NAME
            '''
        }
    }
}
}

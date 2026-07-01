pipeline {
    agent any
    environment {
        DOCKER_CRED = credentials('DockerHub')
    }
    stages {
        stage('fetch-code') {
            steps {
                git branch: 'main', url: 'https://github.com/godofthunder260240-collab/assign4.git'
            }
        }
        stage('build-image') {
            steps {
                sh 'docker build -t atharva260/assign4:${BUILD_NUMBER} .'
            }
        }
        stage('push-image') {
            steps {
                sh 'echo $DOCKER_CRED_PSW | docker login -u $DOCKER_CRED_USR --password-stdin'
                sh 'docker push atharva260/assign4:${BUILD_NUMBER}'
            }
        }
        stage('deploy') {
            steps {
                sh 'kubectl set image deployment/ja1 assign4=atharva260/assign4:${BUILD_NUMBER}'
            }
        }
    }
}

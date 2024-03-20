#!/usr/bin/env groovy
//comment
node ('docker&&linux'){
    stage('Checkout') {

        checkout scmGit{
            branches:
            [[name: 'main']],
            extensions: [],
            userRemoteConfigs: [[url: 'https://github.com/caredh82/cloudcampcicd.git']]
        }
    }

    stage('Build'){
        sh 'exec docker build -t "hello-world-python" -f ./Dockerfile ./'
    }

    stage ('Push') {
        sh "aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 851725481871.dkr.ecr.us-east-1.amazonaws.com"
        sh "docker tag hello-world-python:latest 851725481871.dkr.ecr.us-east-1.amazonaws.com/hello-world-python:3.0"
        sh "docker tag hello-world-python:latest 851725481871.dkr.ecr.us-east-1.amazonaws.com/hello-world-python:latest"
        sh "docker push --all-tags 851725481871.dkr.ecr.us-east-1.amazonaws.com/hello-world-python"
        
    }

}
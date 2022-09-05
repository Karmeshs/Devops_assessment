#!/usr/bin/env groovy
pipeline {
    agent {
        node any
    }

    environment {
		DOCKERHUB_CREDENTIALS =credentials('dockerhub-creds')  //# credentials for docker hub through jenkins
	}

    stages {
        stage('Build Image') {
            when {
                branch 'master'  //only run these steps on the master branch
            }

            // Jenkins Stage to Build the Docker Image
            sh "docker build -t py_app_prediction:latest ."


        }

        stage('Publish Image') {
            when {
                branch 'master'  //only run these steps on the master branch
            }
			sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'

            // Jenkins Stage to Publish the Docker Image to Dockerhub or any Docker repository of your choice.
            sh "docker push py_app_prediction:latest"
			sh 'docker logout'

        }
    }
}
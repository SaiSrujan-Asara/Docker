pipeline {
    agent any
    environment{
        DOCKERHUB_CREDS = credentials('Dockerhub')
    }
    stages {
        stage('Clone Repo') {
            steps {
                checkout scm
                sh 'ls *'
            }
        }
        stage('Build Image') {
            steps {
		sh 'docker build -t potpl/jenkinstest:$BUILD_NUMBER ./pushdockerimage/'
            }
        }
        stage('Docker Login') {
            steps {
                sh 'echo $DOCKERHUB_CREDS_PSW | docker login -u $DOCKERHUB_CREDS_USR --password-stdin'                
                }
            }
        stage('Docker Push') {
            steps {   
                sh 'docker push potpl/jenkinstest:$BUILD_NUMBER'
                }
            }
        }
    post {
		always {
			sh 'docker logout'
		}
	 }
    }


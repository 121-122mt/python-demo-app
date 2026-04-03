pipeline {
    agent any

    environment {
        IMAGE = "manishtiwari123/python-app"
    }
    
    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/121-122mt/python-demo-app.git'
            }
        }

        stage('Build') {
            steps {
                sh 'echo "Build stage running..."'
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Test stage running..."'
            }
        }

        stage('SonarQube Scan') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'sonar-scanner'
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t $IMAGE:$BUILD_NUMBER .'
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh '''
                    docker login -u $USER -p $PASS
                    docker push $IMAGE:$BUILD_NUMBER
                    '''
                }
            }
        }
    }
}

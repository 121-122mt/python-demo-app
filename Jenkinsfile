pipeline {
    agent any

    environment {
        IMAGE = "manishtiwari123/python-app"
    }

        stage('Build') {
            steps {
                sh 'echo "Build stage running1..."'
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

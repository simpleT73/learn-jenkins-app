pipeline {
    agent any

    stages {
        stage('with Docker') {
            agent{
                docker{
                    image 'node:18-alpine'
                }
            }
            steps {
                sh '''
                    echo 'with docker'
                    npm --version
                '''
            }
        }
        stage('without Docker') {
            steps {
                sh '''
                    echo 'without docker'
                    npm --version
                '''
            }
        }
        
    }
}

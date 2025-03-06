pipeline {
    agent any

    environment {
        NETLIFY_SITE_ID = 'f561d6c4-55b4-40a8-99db-d284ea24aafc'
    }

    stages {
        stage('Build') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo "================Building the project================"
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }


        stage('Test')   {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{
                sh '''
                    echo "================Testing the project================"
                    test -f build/index.html
                    npm test
                '''
            }
        }

        stage('Deploy') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo "================Deploying the project================"
                    ping -c 3 8.8.8.8 ; echo $?
                    ping -c 3  registry.npmjs.org ; echo $?
                    ls -la
                    node --version
                    npm --version
                    npm install netlify-cli --save-dev
                '''
            }
        }


    }
    post {
        always{
            junit 'test-results/junit.xml'
        }
    }
}

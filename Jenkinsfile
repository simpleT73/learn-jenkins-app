pipeline {
    agent any

    stages {
        // stage('Build') {
        //     agent{
        //         docker{
        //             image 'node:18-alpine'
        //             reuseNode true
        //         }
        //     }
        //     steps {
        //         sh '''
        //             echo "================Building the project================"
        //             ls -la
        //             node --version
        //             npm --version
        //             npm ci
        //             npm run build
        //             ls -la
        //         '''
        //     }
        // }


        // stage('Test')   {
        //     agent{
        //         docker{
        //             image 'node:18-alpine'
        //             reuseNode true
        //         }
        //     }
        //     steps{
        //         sh '''
        //             echo "================Testing the project================"
        //             test -f build/index.html
        //             npm test
        //         '''
        //     }
        // }

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
                    ip addr
                    ping -c 1  https://registry.npmjs.org ; echo $?
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

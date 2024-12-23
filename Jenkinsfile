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
                    interfaceName=$(ip -o link show | awk -F': ' '{print $2}' | grep -i if4)
                    nmcli connection modify "$interfaceName" ipv4.dns "8.8.8.8"
                    ping -c 10 8.8.8.8 ; echo $?
                    ping -c 10  registry.npmjs.org ; echo $?
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

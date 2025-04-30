pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                ls -alh
                node --version
                npm --version
                npm ci
                npm run build
                ls -alh
                '''
            }
        }
        stage ('Test')
        agent {
            docker {
                image 'node:18-alpine'
                reuseNode true
            }
            steps {
                sh '''
                if [ -e build/index.html ]; then echo "Index.html exists"; fi
                npm test
                '''
            }
        }
    }
}

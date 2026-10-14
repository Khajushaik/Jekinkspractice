pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Khajushaik/Portfolio.git'
            }
        }
        stage('Fixing') {
            steps {
                def container_name = "portfolio"
                sh '''
                     docker stop ${container_name}
                     docker rm -f ${container_name}
                     '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker compose down || true
                    docker compose up -d
                '''
            }
        }

        stage('Verify') {
            steps {
                sh '''
                    docker ps
                    curl -I http://35.153.181.88:1601/
                '''
            }
        }
    }
}

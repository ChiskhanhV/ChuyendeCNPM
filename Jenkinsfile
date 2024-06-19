pipeline {
    agent any

    environment {
        CONTAINER_NAME="my-app"
        DATABASE_NAME="MyDatabase"
        DATABASE_PASSWORD="vck12345"
        DATABASE_ROOT_PASSWORD="vck12345"
        DATABASE_USER = "admin"
    }

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'f343e468-90c0-476f-8ff2-8df9b2e1a608', url: 'https://github.com/ChiskhanhV/ChuyendeCNPM.git', branch: 'main'
            }
        }

        stage('Build and Deploy') {
            steps {
                script {
                    bat 'docker-compose down'
                    bat 'docker-compose up --build'
                }
            }
        }

        stage('Post-deploy Cleanup') {
            steps {
                bat 'docker system prune -f'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/logs/**', allowEmptyArchive: true
        }
    }
}

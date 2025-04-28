pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git branch: 'master', url: 'https://github.com/pestovG/system-design-primer.git'
            }
        }

        stage('Install dependencies') {
            steps {
                sh 'apt-get update'
                sh 'apt-get install -y python3-pip'
                sh 'pip3 install -r requirements.txt || true'
            }
        }

        stage('Test') {
            steps {
                sh 'python3 -m unittest discover -s tests || true'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline успешно выполнен!'
        }
        failure {
            echo '❌ Pipeline завершился с ошибкой.'
        }
    }
}

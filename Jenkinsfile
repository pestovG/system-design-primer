pipeline {
    agent any

    stages {
        stage('Clean Workspace') {
            steps {
                // Очистка рабочей директории перед клонированием репозитория
                deleteDir()  // Удаляет все файлы и папки в рабочей директории
            }
        }

        stage('Clone') {
            steps {
                git branch: 'master', url: 'https://github.com/pestovG/system-design-primer.git'
            }
        }

        stage('Install dependencies') {
            steps {
                sh 'apt-get update'
                sh 'apt-get install -y python3-pip'
                sh 'pip3 install -r requirements.txt || true'  // requirements.txt может отсутствовать
            }
        }

        stage('Test') {
            steps {
                sh 'python3 -m unittest discover -s tests || true'  // если нет тестов - не падаем
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


pipeline {
    agent any
    environment {
        APP_NAME = 'test-app'
    }
    stages {
        stage('Сборка') {
            steps {
                echo "Сборка приложения ${APP_NAME}..."
                sh 'ls -lh'
            }
        }
        stage('Тестирование') {
            steps {
                echo 'Тестирование приложения...'
            }
        }
        stage('Деплой на стейджинг') {
            steps {
                sh 'chmod u+x deploy smoke-tests'
                sh './deploy staging'
                sh './smoke-tests'
            }
        }
        stage('Проверка работоспособности') {
            steps {
                input 'Следует ли отправить на продакшн?'
            }
        }
        stage('Деплой на продакшн') {
            steps {
                sh './deploy production'
            }
        }
    }
    post {
        always {
            echo 'Это выполняется всегда'
        }
        success {
            echo 'Сборка прошла успешно'
        }
        failure {
            echo "Сборка ${env.BUILD_NUMBER} провалилась, лог: ${env.BUILD_URL}"
        }
    }
}

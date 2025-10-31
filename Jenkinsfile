// ✅ Jenkins Declarative Pipeline (Windows + Node.js 프로젝트용)
pipeline {
    agent any

    environment {
        PATH = "C:\\Program Files\\nodejs;%PATH%"
    }

    stages {
        stage('Checkout') {
            steps {
                echo "📦 Git 저장소에서 코드 가져오는 중..."
                checkout scm
            }
        }

        stage('Install') {
            steps {
                bat '''
                echo === INSTALL 단계 시작 ===
                SET PATH=C:\\Program Files\\nodejs;%PATH%
                npm install
                '''
            }
        }

        stage('Test') {
            steps {
                bat '''
                echo === TEST 단계 시작 ===
                SET PATH=C:\\Program Files\\nodejs;%PATH%
                set CI=true
                npm test -- --passWithNoTests
                '''
            }
        }

        stage('Start') {
            when {
                anyOf {
                    branch 'main'
                    expression { env.GIT_BRANCH == 'origin/main' }
                }
            }
            steps {
                bat '''
                echo === START 단계 시작 ===
                SET PATH=C:\\Program Files\\nodejs;%PATH%
                npm run start
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline 성공적으로 완료!'
        }
        failure {
            echo '❌ Pipeline 실패!'
        }
    }
}
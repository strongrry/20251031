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

        stage('Build') {
            when {
                anyOf {
                    branch 'main'
                    expression { env.GIT_BRANCH == 'origin/main' }
                }
            }
            steps {
                bat '''
                echo === BUILD 단계 시작 ===
                SET PATH=C:\\Program Files\\nodejs;%PATH%
                npm run build
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

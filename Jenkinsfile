// ✅ Jenkins Declarative Pipeline (Windows + Node.js 프로젝트용)
pipeline {
    agent any

    // 🌍 Node.js 경로 설정 (Windows 전용)
    environment {
        PATH = "C:\\Program Files\\nodejs;%PATH%"
    }

    stages {
        // 🗂️ 1️⃣ Git 저장소에서 코드 가져오기
        stage('Checkout') {
            steps {
                echo "📦 Git 저장소에서 코드 가져오는 중..."
                checkout scm
            }
        }

        // 📦 2️⃣ 의존성 설치
        stage('Install') {
            steps {
                bat '''
                echo === INSTALL 단계 시작 ===
                SET PATH=C:\\Program Files\\nodejs;%PATH%
                npm install
                '''
            }
        }

        // 🧪 3️⃣ 테스트 실행 (테스트 파일 없어도 통과)
        stage('Test') {
            steps {
                bat '''
                echo === TEST 단계 시작 ===
                SET PATH=C:\\Program Files\\nodejs;%PATH%
                npm test --passWithNoTests
                '''
            }
        }

        // 🚀 4️⃣ 애플리케이션 실행 (main 브랜치일 때만)
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

    // 📋 5️⃣ 빌드 결과 후처리
    post {
        success {
            echo '✅ Pipeline 성공적으로 완료!'
        }
        failure {
            echo '❌ Pipeline 실패!'
        }
    }
}
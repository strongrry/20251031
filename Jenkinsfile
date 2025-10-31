// ✅ Jenkins Declarative Pipeline (Windows + Node.js 프로젝트용)
pipeline {
    agent any

    // 🌍 파이프라인 전체에서 공통으로 사용할 환경 변수 설정
    environment {
        // Windows 환경에서 Node.js 경로를 추가
        PATH = "C:\\Program Files\\nodejs;%PATH%"
    }

    // 🏗️ 실제 작업 단계를 정의하는 블록
    stages {

        // 🗂️ 1️⃣ Git 저장소에서 소스 코드 체크아웃
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        // 📦 2️⃣ Node.js 의존성 설치
        stage('Install') {
            steps {
                bat '''
                echo === INSTALL 단계 시작 ===
                SET PATH=C:\\Program Files\\nodejs;%PATH%
                npm install
                '''
            }
        }

        // 🧪 3️⃣ 테스트 실행
        stage('Test') {
            steps {
                bat '''
                echo === TEST 단계 시작 ===
                SET PATH=C:\\Program Files\\nodejs;%PATH%
                npm test
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
                npm start
                '''
            }
        }
    }

    // 📋 파이프라인 완료 후 실행할 후처리(post) 블록
    post {
        success {
            echo '✅ Pipeline 성공적으로 완료!'
        }
        failure {
            echo '❌ Pipeline 실패!'
        }
    }
}
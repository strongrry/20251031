pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Test') {
            steps {
                script {
                    if (isUnix()) {
                        sh '''
                            set -e
                            if ! grep -q "hello" hello.txt; then
                                echo "실패: hello.txt에 'hello' 문자가 없습니다."
                                exit 1
                            fi
                        '''
                    } else {
                        bat '''
                            findstr /i /c:"hello" hello.txt >nul
                            if errorlevel 1 (
                                echo 실패: hello.txt에 'hello' 문자가 없습니다.
                                exit /b 1
                            )
                        '''
                    }
                }
            }
        }

        stage('Run') {
            steps {
                script {
                    if (isUnix()) {
                        sh '''
                            chmod +x main.sh
                            ./main.sh
                        '''
                    } else {
                        // Windows 환경에서는 main.bat을 실행합니다.
                        bat 'main.bat'
                    }
                }
            }
        }
    }

    post {
        success {
            echo '성공'
        }
        failure {
            echo '실패'
        }
    }
}
pipeline {
    agent any

    environment {
        SKIP_CRASH = "true"  // 避免 CrashController 触发异常
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/GeniusDennis1224/spring-petclinic.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'chmod +x mvnw'
                sh './mvnw clean package'
            }
        }
        
        stage('Test & Code Coverage') {
            steps {
                sh './mvnw test -Dtest=!CrashControllerTests'  // 跳过 CrashControllerTests
                sh './mvnw jacoco:report'
            }
        }
        
        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
    
    triggers {
        cron('H/10 * * * 1')  // 每周一，每 10 分钟执行一次
    }
}

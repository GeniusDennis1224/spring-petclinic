pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/GeniusDennis1224/spring-petclinic.git'
            }
        }
        
        stage('Build') {
            steps {
                sh './mvnw clean package'
            }
        }
        
        stage('Code Coverage with Jacoco') {
            steps {
                sh './mvnw test'
                jacoco(execPattern: '**/target/jacoco.exec', classPattern: '**/target/classes', sourcePattern: '**/src/main/java')
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    triggers {
        cron('H/10 * * * 1')
    }
}


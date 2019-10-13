pipeline {
    agent any
    tools {
        maven 'localMaven'
        jdk 'localJDK'
    }

    triggers {
        pollSCM('* * * * *') // Polling Source Control
    }

    stages {
        stage("build") {
            steps {
                bat 'mvn clean verify'
            }
        }
        stage("sonar") {
            steps {
                withSonarQubeEnv('sonarQube') {
                    bat 'mvn sonar:sonar'
                }
                timeout(time: 1, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
            post {
                success {
                    echo 'SONAR PASSED'
                }
                failure {
                    echo 'SONAR FAILED'
                }
            }

        }
        stage("package") {
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage('deployment') {
            steps {
                deploy(adapters: tomcat8(
                        url: 'http://localhost:8090',
                        password: 'tomcat',
                        userName: 'tomcat'
                ), war: '*/target/*.war', contextPath: '/app')
            }
        }

    }
}
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
        stage("package"){
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

        stage('deployment'){
            steps {
                bat 'xcopy **/target/*.war D:\\apache-tomcat-8.5.46\\webapps /E'
            }
        }

    }
}
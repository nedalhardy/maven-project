pipeline {
    agent any
    tools {
        maven 'localMaven'
        jdk 'localJDK'
    }
    stages {
        stage("build & SonarQube analysis") {
            agent any
            steps {
                withSonarQubeEnv('sonarQube') {
                    bat 'mvn clean package sonar:sonar'
                }
            }
        }
        stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
pipeline {
    agent any
    tools {
        maven 'localMaven'
        jdk 'localJDK'
    }
    stages {
        stage ('build'){
            steps {
                 bat 'mvn clean install'
            }
        }
        stage('Sonarqube') {
            environment {
                scannerHome = tool 'localSonar'
            }
            steps {
                withSonarQubeEnv('sonarQube') {
                    bat "${scannerHome}/bin/sonar-scanner"
                }
                timeout(time: 10, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
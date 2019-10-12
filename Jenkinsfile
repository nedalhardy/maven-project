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
    }
}
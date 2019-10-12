pipeline {
    agent any
    tools {
        maven 'localMaven'
    }
    stages {
        stage ('build'){
            steps {
                 bat 'mvn clean install'
            }
        }
    }
}
pipeline {
    agent any
    tools {
        maven 'localMaven'
    }
    stages {
        stage ('build'){
            steps {
                 sh 'mvn clean install'
            }
        }
    }
}
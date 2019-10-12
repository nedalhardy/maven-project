pipeline {
    agent any
    tools {
        maven 'localMaven'
    }
    stages {
        stage ('build'){
            steps {
                 bash 'mvn clean install'
            }
        }
    }
}
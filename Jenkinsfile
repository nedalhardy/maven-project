pipeline {
    agent any
    tools {
        maven 'localMaven'
        jave 'localJDK'
    }
    stages {
        stage ('build'){
            steps {
                 bat 'mvn clean install'
            }
        }
    }
}
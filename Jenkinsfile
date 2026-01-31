pipeline {
    agent any

    triggers {
        githubPush()   
    }

    stages {

        stage('Clone') {
            steps {
                git branch: 'develop', url: 'https://github.com/Fatih-Othmane/cargo-tracker-UM6P1.git'
            }
        }

        stage('Build & Test with Coverage') {
            steps {
                bat 'mvn clean verify'
            }
        }

        
    }
//
    post {
        success {
            echo 'Build et analyse terminés avec succès !'
        }
        failure {
            echo 'Échec du build ou des tests.'
        }
    }
}

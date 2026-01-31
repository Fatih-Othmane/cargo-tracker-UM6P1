pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {

        stage('1 - Clone Repository') {
            steps {
                git branch: 'develop',
                    url: 'https://github.com/Fatih-Othmane/cargo-tracker-UM6P1.git'
            }
        }

        stage('2 - Compile Project') {
            steps {
                bat 'mvn clean compile'
            }
        }

        stage('3 - Run Unit Tests') {
            steps {
                bat 'mvn test'
            }
        }

        stage('4 - Package Application') {
            steps {
                bat 'mvn package'
            }
        }

        stage('5 - SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQubeServer') {
                    bat 'mvn clean verify sonar:sonar'
                }
            }
        }
    }

    post {
        always {
            junit 'target/surefire-reports/*.xml'
        }
        success {
            echo 'BUILD SUCCESS'
        }
        failure {
            echo 'BUILD FAILURE'
        }
    }
}

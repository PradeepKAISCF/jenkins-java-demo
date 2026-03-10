pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Deploy') {
            when {
                expression { currentBuild.currentResult == 'SUCCESS' }
            }
            steps {
                echo 'Deploying application (simulation)...'
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'target/*.jar'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}

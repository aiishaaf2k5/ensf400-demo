pipeline {
    agent any
    
    environment {
        // Define your secret here (replace 'aisha-secret' with the actual credential ID from Jenkins)
        MY_SECRET = credentials('aisha')  // Secret ID from Jenkins credentials store
    }

    triggers {
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'chmod +x gradlew'
                sh './gradlew clean build -x test'
            }
        }

        stage('Test') {
            steps {
                sh './gradlew test'
            }
            post {
                always {
                    junit '**/build/test-results/test/*.xml'
                }
            }
        }

        stage('Generate Javadocs') {
            steps {
                sh './gradlew javadoc'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Simulating deploy to production...'
                sh 'sleep 5'
                // Example usage of the secret in a deploy step (don't

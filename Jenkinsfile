pipeline {
    agent any

    triggers {
        // Trigger build when changes are pushed to GitHub
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                // Check out code from the repository
                checkout scm
            }
        }

        stage('Restore') {
            when {
                // Execute only when changes are pushed to the main branch
                branch 'main'
            }
            steps {
                // Restore NuGet packages
                sh 'dotnet restore'
            }
        }

        stage('Build') {
            when {
                // Execute only when changes are pushed to the main branch
                branch 'main'
            }
            steps {
                // Build the application in Release configuration
                sh 'dotnet build --no-restore --configuration Release'
            }
        }

        stage('Test') {
            when {
                // Execute only when changes are pushed to the main branch
                branch 'main'
            }
            steps {
                // Run all unit and integration tests
                sh 'dotnet test --no-build --configuration Release'
            }
        }
    }
}
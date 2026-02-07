pipeline {
    agent any
    
    stages {
        stage('Restore Dependencies') {
            steps {
                bat 'dotnet restore'
            }
            post {
                failure {
                    echo 'Failed to restore dependencies. Please check the error messages above.'
                }
        }
        
        stage('Build') {
            steps {
                bat 'dotnet build --no-restore'
            }
        }
        
        stage('Run Tests') {
            paralel {
                stage('Test Project 1') {
                    steps {
                        bat 'dotnet test TestProject1/TestProject1.csproj --no-build --vertbosity normal'
                    }
                }
                stage('Test Project 2') {
                    steps {
                        bat 'dotnet test TestProject2/TestProject2.csproj --no-build --vertbosity normal'
                    }
                }
                stage('Test Project 3') {
                    steps {
                        bat 'dotnet test TestProject3/TestProject3.csproj --no-build --vertbosity normal'
                    }
                }
            }
        }
    }
    
    post {
        always {
            echo 'Workflow completed successfully.'
        }
    }
}
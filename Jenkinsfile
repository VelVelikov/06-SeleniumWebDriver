pipeline {
    agent any

    stages {
        stage('Checkout the repository') {
            steps {
            //Checkout code from Github and specify branch
            //git branch: 'main', url: 'https://github.com/VelVelikov/06-SeleniumWebDriver'
            checkout scm
            }
        }

        stage('Restore the project') {
            steps {
                sh 'dotnet restore'
            }
        }

        stage('Build the project') {
            steps {
                sh 'dotnet build'
            }
        }

        stage('Run tests in parallel'){
            parallel {
                stage('Project1 UI tests') {
                    steps {
                        sh 'dotnet test TestProject1 --no-build --verbosity normal'
                    }
                }
                stage('Project2 UI tests') {
                    steps {
                        sh 'dotnet test TestProject2 --no-build --verbosity normal'
                    }
                }
                stage('Project3 UI tests') {
                    steps {
                        sh 'dotnet test TestProject3 --no-build --verbosity normal'
                    }
                }
            }
        }

    }

    post {
        success {
            echo 'Build and test succeeded!'
        }
        failure {
            echo 'Build or test failed.'
        }
    }
}
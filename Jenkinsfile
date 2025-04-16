pipeline {
    agent any

    tools {
        sbt 'SBT-1.9.7' // Ensure this matches the name of your SBT tool in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://your-git-repo-url/hello-scala.git' // Replace with your repo
            }
        }

        stage('Build') {
            steps {
                sh 'sbt compile'
            }
        }

        stage('Run') {
            steps {
                sh 'sbt run'
            }
        }
    }

    post {
        success {
            echo 'Build and run succeeded!'
        }
        failure {
            echo 'Build or run failed.'
        }
    }
}

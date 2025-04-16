pipeline {
    agent {
        kubernetes {
            yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    jenkins: slave
spec:
  containers:
    - name: sbt-container
      image: hseeberger/scala-sbt:11.0.20_1.9.7_2.13.12
      command:
        - cat
      tty: true
"""
            defaultContainer 'sbt-container'
        }
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

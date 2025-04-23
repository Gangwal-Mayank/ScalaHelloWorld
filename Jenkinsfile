pipeline {
    
      agent { label 'scala' }

    stages {
        stage('Checkout') {
            steps {
                container('scala-sbt') {
                git 'https://github.com/Gangwal-Mayank/ScalaHelloWorld.git' // Replace with your repo
                }
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

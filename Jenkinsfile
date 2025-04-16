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
    - name: scala-sbt
      image: hseeberger/scala-sbt:11.0.20_1.9.7_2.13.12
      command:
        - cat
      tty: true
      volumeMounts:
        - mountPath: /root/.ivy2
          name: ivy-cache
        - mountPath: /root/.sbt
          name: sbt-cache
        - mountPath: /root/.cache
          name: coursier-cache
  volumes:
    - name: ivy-cache
      emptyDir: {}
    - name: sbt-cache
      emptyDir: {}
    - name: coursier-cache
      emptyDir: {}

"""
            defaultContainer 'sbt-container'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Gangwal-Mayank/ScalaHelloWorld.git' // Replace with your repo
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

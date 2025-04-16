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
      image: sbtscala/scala-sbt:graalvm-ce-22.3.3-b1-java17_1.10.11_3.6.4
      imagePullPolicy: Always
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

pipeline {
    agent any
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        stage('Again Hello') {
            steps{
                echo $PATH
            }
        }
        stage('JAVACHECK') {
            steps{
                sh  java
            }
        }
        }
    }
}

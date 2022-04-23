pipeline {
    agent any
    stages {
        steps('Hello') {
                echo 'Hello World'
        }
        steps('Again Hello') {
                echo $PATH
        }
        steps('JAVACHECK') {
                sh  java
        }
        }
}

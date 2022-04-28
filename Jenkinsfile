pipeline {
        agent any
        stages {
                stage('Hello') {
                        steps {
                                echo 'Hello World'
                        }

                        steps{
                                echo $PATH
                        }
                        steps {
                                sh java
                        }
                }
        }
}

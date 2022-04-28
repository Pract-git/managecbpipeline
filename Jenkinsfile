pipeline {
        agent any
        stages {
                stage {
                        steps('Hello') {
                                echo 'Hello World'
                        }

                        steps('Again Hello') {
                                echo $PATH
                        }
                        steps('JAVACHECK') {
                                sh java
                        }
                }
        }
}

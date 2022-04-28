pipeline {
        agent any
        stages {
                stage('Hello') {
                        steps {
                                echo 'Hello World'
                                echo $PATH
                                sh java - version
                        }
                }
        }
        post {
                always {
                        echo 'This will always run'
                }
                success {
                        echo 'This will run only if successful'
                }
                failure {
                        echo 'This will run only if failed'
                }
                unstable {
                        echo 'This will run only if the run was marked as unstable'
                }
                changed {
                        echo 'This will run only if the state of the Pipeline has changed'
                        echo 'For example, if the Pipeline was previously failing but is now successful'
                }
        }
}

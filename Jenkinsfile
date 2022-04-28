pipeline {
        agent any
        stages {
                stage('Hello') {
                        steps {
                                echo 'Hello World'
                                java -version
                        }
                }
                stage('Download Git Repo'){
                        steps {
                                checkout(
                changelog: false,
                poll: false,
                scm: [
                    $class: 'GitSCM',
                    branches: [[name: '*/master']],
                    extensions:  [
                        [
                            $class: 'CleanBeforeCheckout',
                            deleteUntrackedNestedRepositories: false
                        ]
                    ],
                    gitTool: 'jgit',
                    userRemoteConfigs: [
                        [credentialsId: '83b0a1b6-7049-4574-a91f-0bccf35f6c5e',
                        url: 'https://github.com/Pract-git/managecbpipeline.git']
                    ]
                ]
            )
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

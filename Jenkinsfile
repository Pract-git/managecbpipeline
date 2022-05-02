pipeline {
        agent any
        stages {
                stage('Hello') {
                        steps {
                                echo 'Hello World'
                                sh 'java -version'
                        }
                }
                stage('Download Git Repo') {
                        steps {
                                checkout(
                changelog: false,
                poll: false,
                scm: [
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    extensions:  [
                        [
                            $class: 'CleanBeforeCheckout',
                            deleteUntrackedNestedRepositories: false
                        ],
                         [
                            $class: 'RelativeTargetDirectory',
                            relativeTargetDir: 'manage-cb'
                        ],
                    ],
                    gitTool: 'git',
                    userRemoteConfigs: [
                        [credentialsId: '83b0a1b6-7049-4574-a91f-0bccf35f6c5e',
                    url: 'https://github.com/Pract-git/managecbpipeline.git']
                    ]
                ]
            )
                        }
                }
                stage('install hub') {
                        steps {
                       sh 'wget https://github.com/github/hub/releases/download/v2.14.2/hub-linux-amd64-2.14.2.tgz'
                       sh 'gunzip hub-linux-amd64-2.14.2.tgz'
                       sh 'tar -xvf hub-linux-amd64-2.14.2.tar'
                       sh 'cd hub-linux-amd64-2.14.2/'
                       sh 'install'
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

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
                stage('Invoke Manage Content Bucket') {
                        steps {

                                sh '''#!/bin/bash
                                set -ex
                                function run {
                                local will_deploy
                                local -a args=()
                                if [[ "$Create_Content_Bucket" = "true" ]]  ; then
                                        args+=("--create-content-bucket");
                                fi
                                if [[ "${#args[@]}" -gt 0 ]] ; then
                                        args+=("--coe-repo"); args+=("$repo");
                                        args+=("--role-arn"); args+=("$role");

                                        bash -e manage-content-bucket.sh "${args[@]}"
                                else
                                        echo "No images were selected."
                                        exit 1
                                fi
                                }

                                run "$@"
                                '''
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

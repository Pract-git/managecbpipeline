pipeline {
        agent any

        stages {
                stage('Invoke Manage Content Bucket') {
                        steps {
                        sh '''#!/bin/bash
                        set -ex

                        function run {
                        bash -e echo "$Aws_Account"
                        bash -e echo "$Aws_Region"
                        local -r repo="$coe_account.dkr.ecr.us-east-2.amazonaws.com"
                        local -r role="arn:aws:iam::$coe_account:role/allow-ig-build-service-access-from-other-accounts"
                        #local -r ART_REPO="idgov-docker.svsartifactory.swinfra.net/idmapps"
                        #docker login -u ${ARTIFACTORY_USER} -p ${ARTIFACTORY_PWD} idgov-docker.svsartifactory.swinfra.ne
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

pipeline{
    agent any

    stages{
        stage('Zip the file'){
            steps{
                sh 'rm rf *.zip || echo ""'
                sh 'zip ansible-${BUILD_ID}.zip * --exclude Jenkinsfile'

            }
        }

        stage('Upload Artifact to JFrog'){
            steps{
                sh 'curl -uadmin:AP7iKibFPukTLYzjaqQWMbvj12T -T \
                ansible-${BUILD_ID}.zip "http://54.91.55.104:8081/artifactory/Ansible-repo/ansible-${BUILD_ID}.zip"'
            }
        }

        stage('Publish over SSH'){
            steps{
                sshPublisher(publishers: [sshPublisherDesc(configName: 'Ansibleserver',\
                 transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: \
                  'ls', execTimeout: 120000, flatten: false, makeEmptyDirs: false, \
                   noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: \
                    '.', remoteDirectorySDF: false, removePrefix: '', sourceFiles:\
                     'ansible-${BUILD_ID}.zip')], usePromotionTimestamp: false,\
                      useWorkspaceInPromotion: false, verbose: false)])
            }
        }
    }
}
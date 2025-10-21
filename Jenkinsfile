pipeline{
    agent any

    stages{
        stage('Zip the file'){
            steps{
                sh 'rm rf *.zip || echo ""'
                sh 'zip -r ansible-${BUILD_ID}.zip * --exclude Jenkinsfile'

            }
        }

        stage('Upload Artifact to JFrog'){
            steps{
                sh 'curl -uadmin:AP7iKibFPukTLYzjaqQWMbvj12T -T \
                ansible-${BUILD_ID}.zip \
                "http:///13.222.187.64:8081/artifactory/Ansible-repo/ansible-${BUILD_ID}.zip"'
            }
        }

        stage('Publish to Ansible Server'){
            steps{
                sshPublisher(publishers: [sshPublisherDesc(configName: 'Ansibleserver',\
                 transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: \
                  'unzip -o ansible-${BUILD_ID}.zip', execTimeout: 120000,\
                   flatten: false, makeEmptyDirs: false, \
                   noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: \
                    '.', remoteDirectorySDF: false, removePrefix: '', sourceFiles:\
                     'ansible-${BUILD_ID}.zip')], usePromotionTimestamp: false,\
                      useWorkspaceInPromotion: false, verbose: false)])
            }
        }
    }
}
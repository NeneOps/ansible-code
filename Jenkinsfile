pipeline{
    agent any

    stages{
        stage('Zip the file'){
            steps{
                sh 'zip ansible-${BUILD_ID}.zip * --exclude Jenkinsfile'

            }
        }

        stage('Upload Artifact to JFrog'){
            steps{
                sh 'curl -uadmin:AP7iKibFPukTLYzjaqQWMbvj12T -T \
                ansible-${BUILD_ID}.zip "http://54.91.55.104:8081/artifactory/Ansible-repo/ansible-${BUILD_ID}.zip"'
            }
        }
    }
}
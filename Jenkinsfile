pipeline {
    agent { label 'my-linux-agent' }
    stages {

        stage('Install rsync') {
            steps {
                sh 'which rsync || (apt-get update && apt-get install -y rsync)'
            }
        }
        
        stage('Deploy code folder to remote') {
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: 'remote-ssh', keyFileVariable: 'KEYFILE', usernameVariable: 'USER')]) {
                    sh '''
                        rsync -avz -e "ssh -i $KEYFILE -o StrictHostKeyChecking=no" code/ $USER@172.23.33.192:/home/zijan/work/jenkins_github/
                    '''
                }
            }
        }
    }
}

pipeline {
    agent any
    stages {
        stage('Install rsync') {
            steps {
                sh 'apt get update'  // 查看当前用户
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

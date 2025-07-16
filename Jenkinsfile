pipeline {
    agent any
    stages {
        stage('install rsync') {
            steps {
                sh 'echo $USER && ls -l $KEYFILE && head -5 $KEYFILE'
            }
        }
        
        stage('Deploy code folder to remote') {
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: 'remote-ssh', keyFileVariable: 'KEYFILE', usernameVariable: 'USER')]) {
                    sh '''
                        rsync -avz -e "ssh -i $KEYFILE -o StrictHostKeyChecking=no" code $USER@172.23.33.192:/home/zijan/work/jenkins_github/
                    '''
                }
            }
        }
    }
}

pipeline {
    agent any
    stages {
        stage('Deploy code folder to remote') {
            steps {
                // 需要在 Jenkins 上配置 SSH 凭据，假设ID为 'remote-ssh'
                //sshagent(['remote-ssh']) {
                    sh '''
                        echo "rsync -avz code/ zijan@172.23.33.192:/home/zijan/work/jenkins_github/"
                    '''
                }
            }
        }
    }
}

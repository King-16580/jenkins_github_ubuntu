pipeline {
    agent any
    stages {
        stage('Install rsync') {
            steps {
               script {
                    // 确认目标节点是Linux系统
                    def os = sh(script: 'uname', returnStdout: true).trim()
                    if (os != 'Linux') {
                        error "rsync installation only supported on Linux agents"
                    }
                    
                    // 自动检测包管理器并安装
                    sh '''
                        #!/bin/bash
                        if command -v apt-get &> /dev/null; then
                            echo "Detected Debian/Ubuntu system"
                            sudo apt update
                            sudo apt install -y rsync
                        elif command -v yum &> /dev/null; then
                            echo "Detected RHEL/CentOS system"
                            sudo yum install -y rsync
                        elif command -v dnf &> /dev/null; then
                            echo "Detected Fedora system"
                            sudo dnf install -y rsync
                        elif command -v zypper &> /dev/null; then
                            echo "Detected openSUSE system"
                            sudo zypper install -y rsync
                        else
                            echo "ERROR: Unsupported package manager"
                            exit 1
                        fi
                    '''
                }
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

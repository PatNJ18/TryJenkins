def vm2=[:]
vm2.name = 'vm2'
vm2.host = '192.168.2.42'
vm2.user = 'elevier2'
vm2.port = 22
vm2.password = 'elevier'
vm2.allowAnyHosts = true

def vm3=[:]
vm3.name = 'vm3'
vm3.host = '192.168.2.41'
vm3.user = 'elevier3'
vm3.port = 22
vm3.password = 'elevier'
vm3.allowAnyHosts = true

pipeline {
    agent any
    stages {
        stage("Clone Git Repository") {
            steps {
                sshCommand(remote : vm2, command: "git clone https://github.com/PatNJ18/simple-api.git")

                sshCommand(remote : vm2, command: "git clone https://github.com/PatNJ18/simple-api-robot.git")
                
            }
        }
        stage('Build on VM2') {
            steps {
                sshCommand(remote : vm2, command: "python3 simple-api/test.py")

                sshCommand(remote : vm2, command: "cd simple-api")

                sshCommand(remote : vm2, command: "ls")

                sshCommand(remote : vm2, command: "docker build -t jenkins-container simple-api/")

                sshCommand(remote : vm2, command: "docker run -d -p 5000:5000 --name test-jenkins jenkins-container")

            }
        }
        stage('Testing on VM2') {
            steps {

                sshCommand(remote : vm2, command: "python3 -m robot simple-api-robot/apitest.robot")
                
                sshCommand(remote : vm2, command: "docker build -t registry.gitlab.com/me2742732/testme/simple-api simple-api/")
                
                sshCommand(remote : vm2, command: "docker push registry.gitlab.com/me2742732/testme/simple-api")

            }
        }

        stage('Pre-Prod') {
            steps {
                
                sshCommand(remote : vm2, command: "docker pull registry.gitlab.com/me2742732/testme/simple-api")


                sshCommand(remote : vm2, command: "docker run -d -p 5000:5000 --name simple-api registry.gitlab.com/me2742732/testme/simple-api")


            }
        }

    }
    post {
        always {
            sleep 5
        }
    }
}
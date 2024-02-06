pipeline {
    agent any
    stages {
        stage("Clone Git Repository") {
            steps {
                dir('simple-api') {
                    git(
                        url: "https://github.com/PatNJ18/simple-api.git",
                        branch: "main",
                        poll : true
                    )
                }

                dir('simple-api-robot') {
                    git(
                        url: "https://github.com/PatNJ18/simple-api-robot.git",
                        branch: "main",
                        poll : true
                    )
                }
            }
        }
        stage('Build') {
            steps {
                sh '''
                cd simple-api

                docker build -t jenkins-container ./
                docker run -p -d 8081:5000 --name test-jenkins jenkins-container

                '''
            }
        }
        stage('Testing') {
            sh '''
            python3 /simple-api/tests/test.py

            cd simple-api-robot

            robot apitest.robot
            '''
        }

        
    }
}
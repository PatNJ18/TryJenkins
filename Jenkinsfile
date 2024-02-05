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
                echo "Building.."
                sh '''
                echo "clone repo and build container"
                ls 
                pwd
                '''
            }
        }
        stage('Test') {
            steps {
                sh '''
                docker build -t jenkins-api ./simple-api/
                docker run jenkins-api

                
                '''
            }
        }
    }
}
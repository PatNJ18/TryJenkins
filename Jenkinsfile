pipeline {
    agent none
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
            agent {
                docker {
                    image 'python:3.7-alpine'
                }
            }
            steps {
                sh '''
                cd simple-api
                pip install -r requirements.txt
                python /app/app.py



                '''
            }
        }
    }
}
pipeline {
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
    }
}
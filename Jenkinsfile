pipeline {
    agent {
        docker {
            image 'jenkins/jenkins-agent:latest'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    environment {
        VERSION = '1.0.0' // default version
    }
    stages {
        stage('Scan GitHub SCM') {
            steps {
                checkout scm
            }
        }
        stage('Get or Create Version Number') {
            steps {
                script {
                    // This is a placeholder. You'll need to replace this with your own logic
                    // for getting or creating the version number from/in GitHub.
                    VERSION = sh(script: 'echo "1.0.$BUILD_NUMBER"', returnStdout: true).trim()
                    echo "Version: ${VERSION}"
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    def dockerImage = docker.build("my-image:${VERSION}")
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    // Run the Docker container, mapping container port 8080 to host port 3000
                    docker.image("my-image:${VERSION}").run('-p 3000:8080')
                }
            }
        }
    }
}

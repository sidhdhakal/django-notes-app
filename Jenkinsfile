@Library('Shared') _

pipeline {
    agent any

    stages {
        stage("Code clone") {
            steps {
                script {
                    clone("https://github.com/LondheShubham153/django-notes-app.git", "main")
                }
            }
        }

       stage('Build') {
    steps {
        script {
            build(imageName: 'siddhartha54/notes-app', imageTag: 'latest')
        }
    }
}

stage('Push') {
    steps {
        script {
            pushDocker(
                credentials: 'cred',
                imageName: 'siddhartha54/notes-app',
                imageTag: 'latest'
            )
        }
    }
}


      stage("Deploy") {
    steps {
        script {
            echo "Deploying Docker container on localhost"

            // Stop and remove any running container named notes-app (optional, to avoid conflicts)
            sh '''
                docker stop notes-app || true
                docker rm notes-app || true
            '''

            // Run container in detached mode, mapping port 8000 (or your app port) to localhost
            sh '''
                docker run -d --name notes-app -p 8000:8000 siddhartha54/notes-app:latest
            '''

            echo "App deployed and running on localhost:8000"
        }
    }
}

    
    }
    
}

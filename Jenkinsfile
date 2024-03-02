pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/my_website.zip'
            }
        }
        stage('Build Docker Image') {
            when {
                branch 'main'
            }
            steps {
                script {
                    def app = docker.build("davidgnamus/my_website")
                    app.inside {
                        sh 'echo $(curl http://34.244.27.22:8080)'
                    }
                }
            }
        }
    }
}

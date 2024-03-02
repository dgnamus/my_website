pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
        }
        stage('Build Docker Image') {
            when {
                branch 'master'
            }
            steps {
                script {
                    def app = docker.build("davidgnamus/train-schedule")
                    app.inside {
                        sh 'echo $(curl http://localhost:8080)'
                    }
                }
            }
        }
    }
}

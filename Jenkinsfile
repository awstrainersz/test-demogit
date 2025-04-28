pipeline {
    agent any
    tools {
        nodejs "mynodejs"
    }
    environment {
        NODE_ENV = "production"
    }
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Dev') {
            steps {
                git 'https://github.com/awstrainersz/test-demogit'
                echo 'Content of my file is:'
                sh 'cat file1.txt'
            }
        }
        stage('Node Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Save Artifacts') {
            environment{
                NODE_ENV= "stage"
            }
            steps {
                archiveArtifacts artifacts: '*.txt', followSymlinks: false
                echo NODE_ENV
            }
        }
        stage('Stage with Secret') {
            steps {
                withCredentials([string(credentialsId: 'mysecret', variable: 'PRODUCTION_SECRET')]) {
                    echo "${PRODUCTION_SECRET}"
                    script{
                        println " The Secret value is : ${PRODUCTION_SECRET}"
                    }
                }
            }
        }
    }
}

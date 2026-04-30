pipeline {
    agent any

    tools {
        maven 'Maven3'
        jdk 'Java21'
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-creds',
                    url: 'https://github.com/Tallal-Arif/my-web-app.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy') {
            steps {
                deploy adapters: [tomcat9(
                    credentialsId: 'tomcat-creds',
                    path: '',
                    url: 'http://localhost:8080'
                )],
                contextPath: 'my-web-app',
                war: '**/*.war'
            }
        }
    }
}

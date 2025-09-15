pipeline {
    agent any

    tools {
        jdk 'JDK17'       // Name you configured in Global Tool Configuration
        maven 'Maven3'    // Name must match exactly in Global Tool Configuration
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/muge-ms1/jenkins-repo.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
    }
}

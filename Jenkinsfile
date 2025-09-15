pipeline {
    agent any

    tools {
        jdk 'JDK21'       // Use the exact name from Global Tool Configuration
        maven 'MAVEN3'    // Use the exact name from Global Tool Configuration
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

pipeline {
    agent any

    tools {
        jdk 'JDK21'
        maven 'MAVEN3'
    }

stage('Checkout') {
    steps {
        git branch: 'main', url: 'https://github.com/muge-ms1/jenkins-repo.git'
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

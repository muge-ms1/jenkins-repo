pipeline {
    agent any                     // run on any available agent (your Jenkins container)
    
    // Tools names must match what you configured in Manage Jenkins → Global Tool Configuration
    tools {
        jdk 'JDK21'               // name you set for JDK in Jenkins GUI
        maven 'Maven3'           // name you set for Maven in Jenkins GUI
    }

    environment {
        MAVEN_OPTS = '-Xmx1024m'  // optional: tweak JVM for Maven
    }

    options {
        // keep only last 10 builds to conserve space
        buildDiscarder(logRotator(numToKeepStr: '10'))
        // fail fast if pipeline times out
        timeout(time: 30, unit: 'MINUTES')
    }

    stages {
        stage('Checkout') {
            steps {
                // clones the repository that contains this Jenkinsfile (if you configured Pipeline from SCM)
                checkout scm
            }
        }

        stage('Build & Unit Tests') {
            steps {
                // -B = batch mode (no interactive prompts), fail fast on errors
                sh 'mvn -B clean test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn -B package'
            }
        }

        stage('Archive artifacts & test results') {
            steps {
                // archive produced jars
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                // publish JUnit test results so Jenkins shows test reports
                junit 'target/surefire-reports/*.xml'
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded ✅'
        }
        failure {
            echo 'Pipeline failed ❌'
            // optional: collect workspace for debugging
            archiveArtifacts artifacts: '**/logs/*.log', allowEmptyArchive: true
        }
        always {
            // clean workspace on agent (if using ephemeral agents)
            cleanWs()
        }
    }
}

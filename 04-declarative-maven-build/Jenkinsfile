#!/usr/bin/env groovy

// An example of a declarative syntax pipeline for running a maven build

pipeline {
    // Agent to start on (can be changed later in the pipeline
    agent { label 'master' }

    // Define tools to be used in this pipeline
    tools {
        // The M3 maven tool must be already configured in
        // Manage Jenkins -> Global Tool Configuration -> Maven
        maven 'M3'
    }

    // Global options for configuration applied to the whole job
    options {
        // Keep only 10 last build
        buildDiscarder(logRotator(numToKeepStr:'10'))

        // Timeout after 30 minutes
        timeout(time: 30, unit: 'MINUTES')
    }

    // Main build steps
    stages {
        stage('Clone sources') {
            steps {
                git 'https://github.com/JFrogDev/project-examples'
            }
        }
        stage('Maven build') {
            steps {
                sh 'cd maven-example; mvn -Dmaven.test.failure.ignore clean package'
            }
        }
        stage('Test report') {
            steps {
                junit 'maven-example/**/target/surefire-reports/TEST-*.xml'
            }
        }
        stage('Archive') {
            steps {
                archive 'maven-example/**/target/*.war'
            }
        }
    }

    // Post build actions
    post {
        always {
            echo "Always cleanup..."
        }

        success {
            echo "Good build. Send email..."
        }

        failure {
            echo "Failed build. Send email..."
        }
    }
}

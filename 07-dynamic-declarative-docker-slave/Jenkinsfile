#!/usr/bin/env groovy

// An example of using a dynamically allocated Docker slave per stage
// in a declarative syntax pipeline

pipeline {
    agent { label 'master' }
    stages {
        stage('Alpine build') {
            agent {
                docker {
                    label 'master'
                    image 'maven:3-alpine'
                }
            }
            steps {
                echo '====== Running in Alpine ======'
                sh 'cat /etc/os-release'
                sh 'mvn --version'
            }
        }
        stage('Debian build') {
            agent {
                docker {
                    label 'master'
                    image 'openjdk:8-jre'
                }
            }
            steps {
                echo '====== Running in Debian ======'
                sh 'cat /etc/os-release'
                sh 'java -version'
            }
        }
    }
}

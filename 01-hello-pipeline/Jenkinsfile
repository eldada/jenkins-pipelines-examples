#!/usr/bin/env groovy

// A dead simple example of a two stage pipeline

node {
    stage('Hello') {
        echo 'This is the first stage!'
    }
    stage('Jenkins') {
        echo 'This is the second stage!'
        echo 'Job environment'
        sh 'env | sort'
    }
    stage('World') {
        echo 'This is the third stage!'
    }
}

#!/usr/bin/env groovy

pipeline {
    agent any
    tools {
        nodejs "node"
    }
    stages {
        
        stage('Build') {
            steps {
                sh 'yarn'
            }
        }
        stage('Test') {
            steps {
                sh 'yarn run test'
                sh 'yarn run ci-test'
            }
        }
    }
}

#!/usr/bin/env groovy

pipeline {
    agent any
    tools {
        nodejs "NodeJS 15.7.0"
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

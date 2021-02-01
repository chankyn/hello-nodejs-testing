#!/usr/bin/env groovy

pipeline {
    agent any

    tools {
        nodejs "node"
    }
    
    stages {
        
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'npm run test'
                sh 'npm run ci-test'
            }
        }
    }
}

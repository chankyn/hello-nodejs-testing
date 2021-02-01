#!/usr/bin/env groovy

pipeline {
    agent any
  
    stages {
        
        stage('Build') {
            steps {
                withGradle {
                    sh 'yarn'
                }
            }
        }
        stage('Test') {
            steps {
                sh 'yarn run test'
            }
        }
    }
}

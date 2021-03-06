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
            post {
                always {
                    step([
                        $class: 'CloverPublisher',
                        cloverReportDir: 'coverage',
                        cloverReportFileName: 'clover.xml',
                        healthyTarget: [methodCoverage: 70, conditionalCoverage: 80, statementCoverage: 80], // optional, default is: method=70, conditional=80, statement=80
                        unhealthyTarget: [methodCoverage: 50, conditionalCoverage: 50, statementCoverage: 50], // optional, default is none
                        failingTarget: [methodCoverage: 0, conditionalCoverage: 0, statementCoverage: 0]     // optional, default is none
                    ])
                    step([$class: "TapPublisher", testResults: "*.tap"])
                }
            }
        }
        stage('Security') {
            steps {
                sh 'trivy filesystem -f json -o trivy-fs.json .'
                sh 'trivy image -f json -o trivy-image.json hello-brunch'
            }
            post {
                always {
                    recordIssues enabledForFailure: true, aggregatingResults:true, tool: trivy(pattern: 'trivy*.json')
                }
            }
        }
    }
}

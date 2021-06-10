pipeline {
    agent any

    environment {
        JAVA_HOME = '/usr/lib/jvm/java'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Hello'
                sh 'mvn compile'
            }
        }
        stage('Test') {
            steps {
                wrap([$class: 'Xvfb', debug: true, displayName: 50, offsetName: 0]) {
                    sh 'mvn test'
                }
            }
        }
        stage('Report') {
            steps {
                step([$class: 'Publisher', escapeExceptionMsg: true, escapeTestDescp: true, failureOnFailedTestConfig: false, reportFilenamePattern: '**/testng-results.xml', showFailedBuilds: false, thresholdMode: 2, unstableSkips: 100, failedSkips: 100, unstableFails: 0, failedFails: 100])
            }
        }
        stage('Post_Actions') {
            steps {
                echo 'Tests finished'
            }
        }
    }
}

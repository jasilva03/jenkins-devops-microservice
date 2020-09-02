//SCRIPTED


//DECLARATIVE
pipeline {
    agent any
    //agent { docker { image 'maven:3.6.3'} }
    //agent { docker { image 'node:13.8'} }
    environment {
        dockerHome= tool 'myDocker'
        mavenHome= tool 'myMaven'
        PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn --version'
                sh 'docker --version'
                echo "Build"
            }
        }
        stage('Test') {
            steps {
                echo "Test"
            }
        }
        stage('Integration Test') {
            steps {
                echo "Integration Test"
            }
        }
    }
    post {
        always {
            echo 'I am awesome.  I run always'
        }
        success {
            echo 'I run when you are successful'
        }
        failure {
            echo 'I run when you fail'
        }
    }
}

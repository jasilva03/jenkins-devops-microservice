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

        stage('Checkout') {
            steps {
                sh 'mvn --version'
                sh 'docker --version'
                echo "Build"
            }
        }

        stage('Compile') {
            steps {
                sh "mvn clean compile"
            }
        }

        stage('Test') {
            steps {
                sh "mvn test"
            }
        }

        stage('Integration Test') {
            steps {
                sh "mvn failsafe:integration-test failsafe:verify"
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

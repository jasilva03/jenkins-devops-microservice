//SCRIPTED


//DECLARATIVE
pipeline {
    //agent any
    agent { docker { image 'maven:3.6.3'} }
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

        stage('Package') {
            steps {
                sh "mvn package -DskipTest"
            }
        }

        stage('Build Docker Image') {
            steps {
                //"docker build -t jasilva03/currency-exchange-devops:$env.BUILD_TAG"
                script {
                    dockerImage = docker.build("jasilva03/currency-exchange-devops:${env.BUILD_TAG}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('', 'dockerHub') {
                        dockerImage.push();
                        dockerImage.push('latest');
                    }
                }
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

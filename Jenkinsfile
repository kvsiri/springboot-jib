pipeline {
    agent any
    
    stages {
        stage('SCM') {
            steps {
                git url: 'https://github.com/kvsiri/springboot-jib.git'
            }
        }
        stage('Compile') {
            steps {
                withMaven(maven:'Maven 3.5') {
                        sh 'mvn clean compile'
                }
            }
        }
        stage('Unit Tests') {
            steps {
                withMaven(maven:'Maven 3.5') {
                        sh 'mvn clean compile'
                }
            }
        }
        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('My SonarQube Server') {
                    withMaven(maven:'Maven 3.5') {
                        sh 'mvn sonar:sonar'
                    }
                }
            }
        }
        stage('Build Docker Image & Push to DockerHub') {
            steps {
                
                withMaven(maven:'Maven 3.5') {
                        sh 'mvn jib:build -Dimage=kamalakarv/springboot-jib:${project.version}-${BRANCH_NAME}-${BUILD_NUMBER}'
                }
            }
        }
    }

}
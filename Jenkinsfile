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
                        sh 'mvn jib:build -Dimage=kamalakarv/springboot-jib:$BRANCH_NAME-$BUILD_NUMBER'
                }
            }
        }
        stage('Get Image id') {
            
            steps {
        
                script {
                    sh 'docker pull kamalakarv/springboot-jib:$BRANCH_NAME-$BUILD_NUMBER'
                    def IMAGE_ID = sh(script: "docker images | grep -E '^kamalakarv/springboot-jib' | head -1 | awk '{print \$3}'", returnStdout:true).trim()
                    env.IMAGE_ID = IMAGE_ID
                        }
            }
        }
        
        stage('Get Image Vulns - Qualys Plugin') { 
            steps {
                getImageVulnsFromQualys useGlobalConfig:true,
                imageIds: env.IMAGE_ID
            }
        }
    }   

}
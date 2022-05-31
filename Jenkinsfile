pipeline {
    agent any

    tools{
      maven "Maven"
    }
    stages {

          stage('Checkout source code') {
              steps{
            checkout scm
          }}
        stage('SonarQube Analysis') {
          steps{
          withSonarQubeEnv(installationName: 'sonar') {
            bat "mvn -e clean install sonar:sonar -Dsonar.projectKey=Dhiren-sys_hello-world_AYETxN-8KimPFJCr5F9S"
            }
          }
        }

        stage("Quality Gate check") {
          steps {
            timeout(time: 2, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'            
            }
          }
        }
        
        stage('Deploy to UAT') {
            steps {
                    deploy adapters: [tomcat8(credentialsId: 'Container deployer', path: '', url: 'http://192.168.3.18:8080')], contextPath: null, war: 'webapp\\target\\*.war'
            }
        }
        stage('Deploy to Prod') {
            steps {
                    input 'Do you want to proceed this in Prod'
                   deploy adapters: [tomcat8(credentialsId: 'Container deployer', path: '', url: 'http://192.168.3.19:8080')], contextPath: null, war: 'webapp\\target\\*.war'
            }
        }
    }
}

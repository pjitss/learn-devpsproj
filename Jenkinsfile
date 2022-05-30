pipeline {
   agent any

    tools{
      maven "Maven"
    }

    stages {
        stage('SCM') {
            steps {
            checkout scm
            }
        }
        stage('SonarQube Analysis') {
          steps{
          withSonarQubeEnv(installationName: 'sonar') {
            bat "mvn -e clean install sonar:sonar -Dsonar.projectKey=Dhiren-sys_hello-world_AYETxN-8KimPFJCr5F9S"
          }}
        }
      }
    }

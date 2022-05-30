pipeline {
    agent any

node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    //def mvn = tool 'Default Maven';
    withSonarQubeEnv() {
      bat "D:/devops-practices/maven/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=Dhiren-sys_hello-world_AYETxN-8KimPFJCr5F9S"
    }
  }
}
    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/Dhiren-sys/hello-world.git'

                // Run Maven on a Unix agent.
                sh "/jenkins/maven/bin/mvn -Dmaven.test.failure.ignore=true clean install"

                // To run Maven on a Windows agent, use
                // bat "/jenkins/maven/bin/mvn -Dmaven.test.failure.ignore=true clean install"
            }

        }
        
        stage('Deploy') {
            steps {
                    deploy adapters: [tomcat8(credentialsId: 'container-deployer', path: '', url: 'http://10.242.1.237:8085/')], contextPath: null, onFailure: false, war: '**/*.war'
            }
        }
        stage('Deploy to Prod') {
            steps {
                    input 'Do you want to proceed this in Prod'
                    deploy adapters: [tomcat8(credentialsId: 'container-deployer', path: '', url: 'http://10.242.1.209:8080/')], contextPath: null, onFailure: false, war: '**/*.war'
            }
        }
    }
}

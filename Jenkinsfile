pipeline {
    agent any

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

node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def mvn = tool 'MAVEN';
    withSonarQubeEnv('sonar') {
      bat "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=Dhiren-sys_hello-world_AYETxN-8KimPFJCr5F9S"
    }
  }
}

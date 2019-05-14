pipeline {
  agent any
  stages {
    stage('devopstest') {
      steps {
        git(url: 'https://github.com/princejoseph1978/MyTestProjects', branch: 'master', changelog: true, credentialsId: 'b5b61d717b7fffe9c880a483321d0056f8cc9561')
      }
    }
  }
}
pipeline {
  agent any
  stages {
    stage('Source From Git') {
      steps {
        git(url: 'https://github.com/princejoseph1978/MyTestProjects', branch: 'master', changelog: true, credentialsId: 'b5b61d717b7fffe9c880a483321d0056f8cc9561')
      }
    }
    stage('Nuget Restore') {
      steps {
        bat 'H:\\Install\\nuget.exe restore "%JENKINS_HOME%\\workspace\\MyTestProjects_master\\DevopsTest.sln" '
      }
    }
    stage('Unit Test') {
      steps {
        bat 'H:\\Programs\\VisualStudio\\2017\\Common7\\IDE\\CommonExtensions\\Microsoft\\TestWindow\\vstest.console.exe %JENKINS_HOME%\\workspace\\%ITEM_FULL_NAME%\\DevopsTest.Tests\\bin\\Release\\DevopsTest.Tests.dll'
      }
    }
  }
}
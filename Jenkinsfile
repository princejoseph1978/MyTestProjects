pipeline {
  agent any
  stages {
    stage('Source From Git') {
      steps {
        git(url: 'https://github.com/princejoseph1978/MyTestProjects', branch: 'master', changelog: true, credentialsId: 'b5b61d717b7fffe9c880a483321d0056f8cc9561')
      }
    }
    stage('Build') {
      steps {
        changeAsmVer '1.0.0.$BUILD_NUMBER'
        bat(script: '"H:\\Install\\nuget.exe" restore "%JENKINS_HOME%\\workspace\\MyTestProjects_master\\DevopsTest.sln"', label: 'Nuget Restore')
        bat(script: '"H:\\Programs\\VisualStudio\\2017\\MSBuild\\15.0\\Bin\\MSBuild.exe" "%JENKINS_HOME%\\workspace\\MyTestProjects_master\\DevopsTest.sln" /t:Clean;Build /p:Configuration=Release /p:DeployOnBuild=true /p:PublishProfile=FolderProfile', label: 'MsBuild')
      }
    }
    stage('Unit Test') {
      steps {
        bat 'H:\\Programs\\VisualStudio\\2017\\Common7\\IDE\\CommonExtensions\\Microsoft\\TestWindow\\vstest.console.exe %JENKINS_HOME%\\workspace\\MyTestProjects_master\\DevopsTest.Tests\\bin\\Release\\DevopsTest.Tests.dll'
      }
    }
    stage('Deploy') {
      steps {
        bat 'xcopy /I /Y "%JENKINS_HOME%\\workspace\\MyTestProjects_master\\DevopsTest\\bin\\Release\\Publish" "H:\\CodeWorkspace\\PrinceWorkSpace\\Deploy\\DevopsTest\\Test"'
      }
    }
  }
}
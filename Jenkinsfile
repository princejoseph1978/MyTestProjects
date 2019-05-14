pipeline {
  agent any
  stages {
    stage('PullSourceFromGit') {
      steps {
        git(url: 'https://github.com/princejoseph1978/MyTestProjects', branch: 'master', changelog: true, credentialsId: 'b5b61d717b7fffe9c880a483321d0056f8cc9561')
      }
    }
    stage('Build') {
      parallel {
        stage('Restore NuGet') {
          steps {
            bat 'H:\\Install\\nuget.exe restore %PROJECTS_HOME%\\DevopsTest\\DevopsTest.sln'
          }
        }
        stage('MS Build') {
          steps {
            bat 'H:\\Programs\\VisualStudio\\2017\\MSBuild\\15.0\\Bin\\MSBuild.exe %PROJECTS_HOME%\\DevopsTest\\DevopsTest.sln /t:clean;build /p:Configuration=Release'
          }
        }
      }
    }
    stage('MsTest') {
      steps {
        bat 'H:\\Programs\\VisualStudio\\2017\\Common7\\IDE\\CommonExtensions\\Microsoft\\TestWindow\\vstest.console.exe %PROJECTS_HOME%\\DevopsTest\\DevopsTest.Tests\\bin\\Release\\DevopsTest.Tests.dll'
      }
    }
  }
}
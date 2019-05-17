pipeline {
  agent any
  stages {
    stage('Source From Git') {
      steps {
        git(url: '%GIT_URL%', branch: '%GIT_BRANCH%', changelog: true, credentialsId: '9df2a8be7ec25d6da63599237a12ec854e7cc0dc')
      }
    }
    stage('Build') {
      steps {
        changeAsmVer '1.0.0.$BUILD_NUMBER'
        bat(script: '"%NUGET_PATH%" restore "%JENKINS_HOME%\\workspace\\%JOB_NAME:/=_%\\%PROJ_SLN_NAME%"', label: 'Nuget Restore')
        bat(script: '"%MSBUILD_PATH%" "%JENKINS_HOME%\\workspace\\%JOB_NAME:/=_%\\%PROJ_SLN_NAME%" /t:Clean;Build /p:Configuration=Release /p:DeployOnBuild=true /p:PublishProfile=%PUBLISH_PROFILENAME%', label: 'MsBuild')
      }
    }
    stage('Unit Test') {
      steps {
        bat '%UNIT_TESTEXE_PATH% %JENKINS_HOME%\\workspace\\%JOB_NAME:/=_%\\%UNIT_TESTDLL_PATH%'
      }
    }
    stage('Deploy') {
      steps {
        bat(script: 'xcopy /S /Y /I "%JENKINS_HOME%\\workspace\\%JOB_NAME:/=_%\\%PUBLISH_PATH%" "%DEPLOY_PATH%"', label: 'Deploy Files')
        bat(label: 'Create Backup', script: 'xcopy /S /Y /I "%DEPLOY_PATH%" "%DEPLOY_BACKUP_PATH%\\%BACKUP_FOLDER_PREFIX%_%GIT_COMMIT%"')
      }
    }
  }
  environment {
    GIT_URL = 'https://github.com/princejoseph1978/MyTestProjects'
    GIT_BRANCH = 'master'
    GIT_CREDENTIAL_TOKEN = 'b5b61d717b7fffe9c880a483321d0056f8cc9561'
    PROJ_SLN_NAME = 'DevopsTest.sln'
    NUGET_PATH = 'H:\\Install\\nuget.exe'
    MSBUILD_PATH = 'H:\\Programs\\VisualStudio\\2017\\MSBuild\\15.0\\Bin\\MSBuild.exe'
    UNIT_TESTEXE_PATH = 'H:\\Programs\\VisualStudio\\2017\\Common7\\IDE\\CommonExtensions\\Microsoft\\TestWindow\\vstest.console.exe'
    UNIT_TESTDLL_PATH = 'DevopsTest.Tests\\bin\\Release\\DevopsTest.Tests.dll'
    PUBLISH_PROFILENAME = 'FolderProfile'
    PUBLISH_PATH = 'DevopsTest\\bin\\Release\\Publish'
    DEPLOY_PATH = 'H:\\CodeWorkspace\\PrinceWorkSpace\\Deploy\\DevopsTest\\Test'
    DEPLOY_BACKUP_PATH = 'H:\\CodeWorkspace\\PrinceWorkSpace\\Deploy\\DevopsTest\\Backups'
    BACKUP_FOLDER_PREFIX = 'DevopsTest'
  }
}
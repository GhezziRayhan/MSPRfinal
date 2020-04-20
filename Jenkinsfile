pipeline {
  agent any
  stages {
    stage('Checking') {
      parallel {
        stage('Checking Git') {
          steps {
            bat 'D:\\Users\\rayha\\OneDrive\\Bureau\\JenkinsPackaging\\scripts\\CheckGit.bat'
          }
        }

        stage('Checking Files') {
          steps {
            bat 'D:\\Users\\rayha\\OneDrive\\Bureau\\JenkinsPackaging\\scripts\\CheckFiles.bat'
          }
        }

      }
    }

    stage('Maven') {
      parallel {
        stage('Maven Compilation') {
          steps {
            build 'MavenCompilation'
          }
        }

        stage('Maven Test') {
          steps {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
              build 'MavenTest'
            }

          }
        }

      }
    }

    stage('Android Mobile') {
      steps {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          build 'MobileAndroid'
        }

      }
    }

    stage('Test Result') {
      steps {
        bat 'D:\\Users\\rayha\\OneDrive\\Bureau\\JenkinsPackaging\\scripts\\Result.bat'
      }
    }

  }
}
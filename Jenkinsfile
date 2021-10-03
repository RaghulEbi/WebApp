pipeline {
  agent any
  stages {
    stage('dev code pull') {
      steps {
        echo 'Dev code pull'
         git url :'https://github.com/TestLeafInc/WebApp.git'
      }
    }

    stage('dev build') {
      steps {
        echo 'Dev mvn build'
         bat 'start /min StopApp.bat'
            bat 'mvn install'
            bat 'set JENKINS_NODE_COOKIE=dontkillme && start /min StartApp.bat'
      }
    }

    stage('QA test') {
      parallel {
        stage('QA test') {
          steps {
            echo 'QA test starts'
               }
        }

        stage('QA UI test') {
          steps {
            echo 'QA UI test start'
            git url: 'https://github.com/TestLeafInc/WebAppUiAutomation.git'
            sleep (time:10,unit:'SECONDS')
            bat 'mvn test'
          }
        }

        stage('QA API test') {
          steps {
            echo 'QA API test start'
             git url: 'https://github.com/TestLeafInc/WebAppApiAutomation.git'
            sleep (time:10,unit:'SECONDS')
            bat 'mvn test'
          }
        }

      }
    }

    stage('QA approval') {
      steps {
        input(message: 'QA approval ', id: 'Yes', ok: 'No')
      }
    }

    stage('UAT approval') {
      steps {
        input(message: 'UAT approval', id: 'Yes', ok: 'No')
      }
    }

    stage('Prod deploy') {
      steps {
        echo 'Prod deploy '
      }
    }

  }
}

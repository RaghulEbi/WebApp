pipeline {
  agent any
  stages {
    stage('dev code pull') {
      steps {
        echo 'Dev code pull'
      }
    }

    stage('dev build') {
      steps {
        echo 'Dev mvn build'
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
          }
        }

        stage('QA API test') {
          steps {
            echo 'QA API test start'
          }
        }

      }
    }

    stage('QA approval') {
      steps {
        input(message: 'QA approval ', id: 'Yes', ok: 'Yes-good')
      }
    }

    stage('UAT approval') {
      steps {
        input(message: 'UAT approval', id: 'Yes', ok: 'Yes-good')
      }
    }

    stage('Prod deploy') {
      steps {
        echo 'Prod deploy '
      }
    }

  }
}
pipeline {
  agent any
  triggers {
    cron('* 23 * * *')
  }
  stages {
    stage('echo') {
      steps {
        echo 'Triggered'
      }
    }
   }
}

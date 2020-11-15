pipeline {
  agent any
  triggers {
    cront('H/15 * * * *')
  }
  stages {
    stage('echo') {
      steps {
        echo 'Triggered'
      }
    }
   }
}

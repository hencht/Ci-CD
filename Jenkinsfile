pipeline {
  agent any
  parameters {
      choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description '')
      boolenanParam(name: 'executeTests', defaultValue: true, description: '')
  }
  stages {
    stage("build") {
      steps {
        echo 'Building the application...'
      }
    }
    
    stage("test") {
        when {
            expression {
                BRANCH_NAME == 'dev'  || BRANCH_NAME == 'master'
                params.executeTests
            }
        }
      steps {
        echo 'Testing the application...'
      }
    }
    
    stage("deploy") {
      steps {
        echo 'Deploying the application...'
        echo "Deploying ${params.VERSION}"
      }
    }
  }
}

def gv
pipeline {
  agent any
  parameters {
      choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
      booleanParam(name: 'executeTests', defaultValue: true, description: '')
  }
  stages {
    stage("init") {
      steps {
        script {
          gv = load "script.groovy"
        }
      }
    }
    
    stage("build") {
      steps {
        script {
          gv.buildApp()
        }
      }
    }

    stage('Add Config files') {
        steps {
            configFileProvider([configFile(fileId: 'app-version', variable: 'APP-VERSION')]) {
            sh "cat \$APP-VERSION"

            }
           
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
        script {
          gv.testApp()
        }
      }
    }
    
    stage("deploy") {
      steps {
        script {
          gv.deployApp()
        }
      }
    }
  }
}



@Library('shared-library') _
pipeline {
  agent any
  parameters {
      choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
      booleanParam(name: 'executeTests', defaultValue: true, description: '')
  }
  stages {
    stage('Add Config files') {
        steps {
            configFileProvider([configFile(fileId: 'app-version', variable: 'APP_VERSION')]) {
            echo " =========== ^^^^^^^^^^^^ Reading config from pipeline script "
            sh "cat ${env.APP_VERSION}"
            echo "============= ~~~~~~~~~~~ =============="

            }    
        }
    }
    stage("build") {
        when {
            expression {
                BRANCH_NAME == 'dev'  || BRANCH_NAME == 'master'
                params.executeTests
            }
        }
      steps {        
          bumpVersion()
        }
    }
  }
}



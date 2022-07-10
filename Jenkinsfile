@Library('shared-library') _
pipeline {
  agent any
  parameters {
      choice(name: 'VERSION', 
        choices: 
            ['1.1.0', '1.2.0', '1.3.0'], description: '')
      booleanParam(name: 'executeTests', defaultValue: true, description: '')
      
      choice(
        name: 'nextVersionIncrement',
        choices: [
            'Minor',
            'Major'
        ],
        description: 'The version number to increment for the base branch if running against the repos master branch (<Major>.<Minor>.0-SNAPSHOT)'
      )
      string(
        name: 'baseBranch',
        defaultValue: 'master',
        description: 'The branch to create a realse branch from.'
      )
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
                BRANCH_NAME == 'master' || BRANCH_NAME == 'dev1'
                params.executeTests
            }
        }
        steps {        
            script{
                bumpcommithash = bumpVersion branch: params.baseBranch, incrementType: params.nextVersionIncrement
            }
         
        }
    }
  }
}



pipeline {
  agent any
  stages {
    stage('Prep_Environment') {
      steps {
        echo 'Setting Development Environment'
        sh 'id'
        sh 'printenv'
        sh 'ls /usr/local/lib/node_modules/npm/bin'
        sh 'npm -v'
        sh 'ctm -v'
        sh 'echo $PATH'
        sh 'ctm env add Dev "https://cirrocumulus.bmci2t.com:8446/automation-api" "Reggie" "Password"'
        sh 'ctm env show'
        sh 'ctm env set Dev'
        echo 'Environment was set to Dev'
      }
    }

    stage('Validate_Workflow') {
      steps {
        echo 'Validate Workflow Syntax'
        sh '/usr/local/lib/node_modules/npm/bin/ctm build DevJobs.json'
        echo 'Worklow Build Complete'
      }
    }

    stage('Deploy_Workflow') {
      steps {
        echo 'Applying Deploy Descriptor Transform and Running Workflow'
        sh '/usr/local/lib/node_modules/npm/bin/ctm run DevJobs.json DevDeploy.json -e Dev'
        echo 'Worklow Run Complete'
      }
    }

    stage('Clean-up Development Environment') {
      steps {
        echo 'Deleting Development Environment'
        sh '/usr/local/lib/node_modules/npm/bin/ctm env delete Dev'
        echo 'Environment delete Complete'
      }
    }

    stage('Prep_Environment_Prod') {
      steps {
        echo 'Setting Production Environment'
        sh '/usr/local/lib/node_modules/npm/bin/ctm env add Production "https://workbench:8443/automation-api" "workbench" "workbench"'
        sh '/usr/local/lib/node_modules/npm/bin/ctm env show'
        sh '/usr/local/lib/node_modules/npm/bin/ctm env set Production'
        echo 'Environment was set to Prod'
      }
    }

    stage('Deploy_Workflow_Prod') {
      steps {
        echo 'Applying Deploy Descriptor Transform and Running Workflow'
        sh '/usr/local/lib/node_modules/npm/bin/ctm run DevJobs.json ProdDeploy.json -e Production'
        echo 'Worklow Run Complete'
      }
    }

    stage('Clean-up Production Environment') {
      steps {
        echo 'Deleting Production Environment'
        sh '/usr/local/lib/node_modules/npm/bin/ctm env delete Production'
        echo 'Environment delete Complete'
      }
    }

  }
}

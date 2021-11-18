pipeline {
  agent any
  stages {
    stage('Prep_Dev_Environment') {
      steps {
        echo 'Setting Development Environment'
        sh 'id'
        sh 'printenv'
        sh 'ls /usr/local/lib/node_modules/npm/bin'
        sh 'npm -v'
        sh 'ctm -v'
        sh 'echo $PATH'
        sh 'ctm env set demo_sandbox'
        sh 'ctm env show'
        echo 'Environment was set to Dev'
      }
    }
    stage('Validate_Dev_Workflow') {
      steps {
        echo 'Validate Workflow Syntax'
        sh 'ctm build deployjobs.json'
        echo 'Worklow Build Complete'
      }
    }
    stage('Deploy_Workflow') {
      steps {
        echo 'Applying Deploy Descriptor Transform and Running Workflow on dev'
        sh 'ctm run deployjobs.json -e demo_sandbox'
        echo 'Worklow Run Complete'
      }
    }
    stage('Prep_Prod_Environment') {

      steps {
        echo 'Setting Production Environment'
        sh 'ctm env set demo_sandbox'
        echo 'Environment was set to Prod'
      }
    }
    stage('Validate_Prod_Workflow') {
      steps {
        echo 'Validate Workflow Syntax'
        sh 'ctm build deployjobs.json'
        echo 'Worklow Build Complete'
      }
    }
    stage('Deploy_Workflow_Prod') {
      steps {
        echo 'Applying Deploy Descriptor Transform and Running Workflow'
        sh 'ctm run deployjobs.json ProdDeploy.json -e Production'
        echo 'Worklow Run Complete'
      }
    }
  }
}

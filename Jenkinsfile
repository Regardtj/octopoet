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
        sh 'ctm env set demo_sandbox'
        sh 'ctm env show'
        echo 'Environment was set to Dev'
      }
    }

    stage('Validate_Workflow') {
      steps {
        echo 'Validate Workflow Syntax'
        sh 'ctm build genjobs.json'
        echo 'Worklow Build Complete'
      }
    }

    stage('Deploy_Workflow') {
      steps {
        echo 'Applying Deploy Descriptor Transform and Running Workflow on dev'
        sh 'ctm run genjobs.json -e demo_sandbox'
        echo 'Worklow Run Complete'
      }
    }
  }
}

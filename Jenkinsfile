
pipeline {

  options {
    buildDiscarder(logRotator(numToKeepStr: '30', artifactNumToKeepStr: '30'))
  }

  agent {
    node {
      label 'jenkins-agent-java11'
    }
  }

  stages {
    stage('Prep') {
      steps {
        script {
          currentBuild.displayName = "#${env.BUILD_NUMBER}-${env.JOB_BASE_NAME}"
        }
        sendNotifications 'STARTED'
      }
    }

    stage('API lint') {
      steps {
        runApiLint('RAML', 'ramls', 'ramls.raml jsonSchemas.raml', true)
      }
    }

    stage('API schema lint') {
      steps {
        runApiSchemaLint('.', 'codex-next')
      }
    }

    stage('Generate API docs') {
      when {
        anyOf {
          branch 'master'
          branch 'raml1.0'
        }
      }
      steps {
        runApiDoc('RAML', 'ramls', '')
      }
    }

  } // end stages

  post {
    always {
      sendNotifications currentBuild.result
    }
  }

}



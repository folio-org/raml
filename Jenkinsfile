
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

    stage('Lint raml-cop') {
      steps {
        runLintRamlCop()
      }
    }

    stage('API lint') {
      steps {
        runApiLint('RAML', 'ramls', 'ramls.raml jsonSchemas.raml')
      }
    }

    stage('API schema lint') {
      steps {
        runApiSchemaLint('.', 'codex-next')
      }
    }

    stage('Publish API Docs') {
      when {
        anyOf {
          branch 'master'
          branch 'raml1.0'
        }
      }
      steps {
        sh 'python3 /usr/local/bin/generate_api_docs.py -r raml -l info -o folio-api-docs'
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding',
                          accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                          credentialsId: 'jenkins-aws',
                          secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
          sh 'aws s3 sync folio-api-docs s3://foliodocs/api'
        }
      }
    }


  } // end stages

  post {
    always {
      sendNotifications currentBuild.result
    }
  }

}



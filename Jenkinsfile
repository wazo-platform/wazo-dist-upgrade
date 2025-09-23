pipeline {
  agent any
  triggers {
    githubPush()
    pollSCM('H H * * *')
  }
  environment {
    MAIL_RECIPIENTS = 'dev+tests-reports@wazo.community'
  }
  options {
    skipStagesAfterUnstable()
    timestamps()
    buildDiscarder(logRotator(numToKeepStr: '10'))
  }
  stages {
    stage('Debian build and deploy') {
      steps {
        build job: 'build-package-no-arch', parameters: [
          string(name: 'PACKAGE', value: "${JOB_NAME}"),
        ]
      }
    }
    stage ('Sync package') {
      steps {
        sh '''
        REPREPRO=mirror.wazo.community
        ssh \$REPREPRO reprepro-main -v copysrc wazo-dev-buster wazo-dev-bullseye wazo-dist-upgrade
        ssh \$REPREPRO reprepro-main -v copysrc wazo-dev-stretch wazo-dev-bullseye wazo-dist-upgrade
        ssh \$REPREPRO reprepro-main -v copysrc wazo-rc wazo-dev-bullseye wazo-dist-upgrade
        '''
      }
    }
  }
  post {
    failure {
      emailext to: "${MAIL_RECIPIENTS}", subject: '${DEFAULT_SUBJECT}', body: '${DEFAULT_CONTENT}'
    }
    fixed {
      emailext to: "${MAIL_RECIPIENTS}", subject: '${DEFAULT_SUBJECT}', body: '${DEFAULT_CONTENT}'
    }
  }
}

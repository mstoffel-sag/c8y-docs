pipeline {
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
    skipStagesAfterUnstable()
  }
  agent {
    kubernetes {
      inheritFrom 'c8y-hugo'
      defaultContainer 'default'
    }
  }
  parameters {
    string(defaultValue: 'release/r10.4.6-BB', description: 'branch/revison', name: 'BRANCH')
  }
  environment {
    YUM_SRV = 'yum.cumulocity.com'
    YUM_USR = 'hudson'
    YUM_DEST_DIR = '/var/www/staticpage-guides/guides/'
    HUGO_PARAMS = ""
  }

  stages {
    stage('Checkout') {
            steps {
                git branch: "${params.BRANCH}", credentialsId: "jenkins-master", url:'ssh://git@bitbucket.org/m2m/c8y-docs/'
            }
        }
    stage('Build') {
      steps {
        sh '''bash --login
          if [ -f "properties.json" ]
  then
  	DOC_VERSION=$( jq -r '.name' < properties.json )
    hugo ${HUGO_PARAMS} -d ./${DOC_VERSION}
  else
  	echo "Properties not found."
  fi
          '''
      }
    }
    stage('Deploy') {
      steps {
        sshagent(['jenkins-master']) {
          sh '''bash --login
          echo ${params.BRANCH}

          splitBranch = ${params.BRANCH} | sed -e 's/\/.*\///g'

          echo splitBranch

          DOC_VERSION=$( jq -r '.name' < properties.json )
          echo ${DOC_VERSION}
          rsync -e "ssh -o StrictHostKeyChecking=no" -avh ./${DOC_VERSION} ${YUM_USR}@${YUM_SRV}:${YUM_DEST_DIR} --delete
          '''
        }
      }
    }
  }
}

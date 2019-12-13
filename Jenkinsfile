pipeline {
  agent any
  stages {
    stage('Init') {
      steps {
        echo "Github branch is ${BRANCH}"
        sh 'ssh root@${SERVER}'
      }
    }

    stage('Code Coverage') {
      steps {
        echo 'Demo'
      }
    }

    stage('Deploy') {
      steps {
                sh 'ssh ${USER}@${SERVER} "cd ${MAGE_ROOT} && git reset --hard && git checkout origin/${BRANCH} && git pull origin ${BRANCH} && docker-compose run deploy magento-command setup:upgrade && docker-compose run deploy magento-command setup:di:compile && docker-compose run deploy magento-command setup:static-content:deploy -f && docker-compose run deploy magento-command c:c && docker-compose run deploy magento-command c:f"'
      }
    }

  }
}
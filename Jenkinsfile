pipeline {
  agent any
  stages {
    stage('Init') {
      steps {
        echo "Github branch is ${BRANCH}"
        sh 'pwd && composer install && vendor/bin/phpcs --config-set installed_paths vendor/magento/magento-coding-standard/Magento2/ '
      }
    }

    stage('Code Coverage') {
      steps {
        sh '/var/lib/jenkins/tools/hudson.tasks.Ant_AntInstallation/Ant_1.10.7/bin/ant full-build-parallel'
      }
    }

    stage('Deploy') {
      steps {
        sh '''ssh root@10.10.21.180 "cd /var/www/rav-rp \\
&& git pull origin dev \\
&& docker-compose run deploy magento-command setup:upgrade \\
&& docker-compose run deploy magento-command setup:di:compile \\
&& docker-compose run deploy magento-command setup:static-content:deploy -f \\
&& docker-compose run deploy magento-command c:c \\
&& docker-compose run deploy magento-command c:f"'''
      }
    }

  }
}
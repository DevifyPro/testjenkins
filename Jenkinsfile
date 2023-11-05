node {
  stage("Main") {

    checkout scm

    docker.image('bitnami/php-fpm:latest').inside("-e COMPOSER_HOME=/tmp/jenkins-workspace") {

      stage("Prepare folders") {
        sh "mkdir /tmp/jenkins-workspace"
      }

      stage("Get Composer") {
        sh "php -r \"copy('https://getcomposer.org/installer', 'composer-setup.php');\""
        sh "php composer-setup.php"
      }

      stage("Install dependencies") {
        sh "php composer.phar install"
      }

      stage("Run tests") {
        sh "vendor/bin/phpunit"
      }

   }

  }

  // Clean up workspace
  step([$class: 'WsCleanup'])

}

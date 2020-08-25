pipeline {
  agent any
    stages {
      stage ('Build') {
        steps {
          sh 'mvn compile sonar:sonar package'
        }
      }
      stage ('Delivery') {
        steps {
          script {
          sshPublisher(
          publishers: [
            configName:'DO-tomcat',
            transfers [
              sourceFiles:'target/*.war',
              removePrefix:'target/',
              execCommand:'systemctl restart tomcat'
            ]
          ])}
        }
      }
    }
}

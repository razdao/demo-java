pipeline {
  agent any
    stages {
      stage ('Build') {
        steps {
          sh 'mvn compile sonar:sonar package'
        }
      }
      stage ('Delivery') {
        publishers {
          publishOverSsh {
            configName('DO-tomcat')
            transferSet {
              sourceFiles('target/*.war')
              removePrefix('target/')
              execCommand('systemctl restart tomcat')
            }
          }
        }
      }
    }
}

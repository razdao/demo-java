pipeline {
  agent any
    stages {
      stage ('Build') {
        steps {
          sh 'mvn compile sonar:sonar package'
        }
      }
      stage ('Delivery') {
        steps([$class: 'BapSshPromotionPublisherPlugin']) {
          sshPublisher(
            continueOnError: false, failOnError: true,
            publishers: [
              sshPublisherDesc(
                configName: "DO-tomcat",
                verbose: true,
                  transfers: [
                    sshTransfer(sourceFiles: "target/*.war"),
                    sshTransfer(execCommand: "systemctl restart tomcat"),
                  ]
              )
            ]
          )
        }
      }
    }
}

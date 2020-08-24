pipeline {
  agent any
    stages {
      stage ('Build') {
        steps {
          sh 'mvn compile sonar:sonar package'
        }
    }
    post { 
        always { 
            echo 'I will always say Hello again!'
        }
    }
}

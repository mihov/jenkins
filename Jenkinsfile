pipeline {
  agent any
  stages {
    stage('SCM') {
      steps {
        git(url: 'ssh://git@bitbucket.imperiaonline.org:7999/javb/resource-manager.git', branch: 'develop', poll: true, changelog: true)
      }
    }
    stage('Buld') {
      steps {
        withMaven(jdk: '1.8.131', maven: '3.5.0') {
          sh 'mvn clean install'
        }
        
      }
    }
    stage('Static Analisys') {
      steps {
        sh 'mvn findbugs:check'
        findbugs()
      }
    }
  }
}
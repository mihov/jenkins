pipeline {
  agent any
  stages {
    stage('SCM') {
      steps {
        git(url: 'ssh://git@bitbucket.imperiaonline.org:7999/javb/resource-manager.git', branch: 'develop', poll: true, changelog: true)
        sh 'git status'
      }
    }
    stage('Buld') {
      steps {
        withMaven(jdk: 'JAVA', maven: '3.5.0') {
          sh 'mvn clean -P dev deploy'
        }
        
      }
    }
    stage('Checkstyle') {
      steps {
        checkstyle(useDeltaValues: true, usePreviousBuildAsReference: true, useStableBuildAsReference: true)
      }
    }
    stage('Artefacts') {
      steps {
        archiveArtifacts 'target/*.war'
      }
    }
  }
}
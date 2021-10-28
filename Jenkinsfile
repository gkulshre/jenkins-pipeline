pipeline {
  agent any
  stages {
    stage('maven-build') {
      steps {
        git(url: 'https://github.com/gkulshre/war-web-project.git', branch: 'master')
        sh 'mvn package'
        archiveArtifacts '**/*.war'
      }
    }

    stage('maven-test-env') {
      steps {
        copyArtifacts(fingerprintArtifacts: true, projectName: 'maven-build', selector: lastSuccessful())
      }
    }

  }
  options {
    copyArtifactPermission('maven-test-env')
  }
}
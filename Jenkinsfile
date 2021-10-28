pipeline {
  agent any
  stages {
    stage('maven-build-new') {
      steps {
        git(url: 'https://github.com/gkulshre/war-web-project.git', branch: 'master')
        sh 'mvn package'
        archiveArtifacts '**/*.war'
      }
    }

    stage('maven-test-env') {
      steps {
        copyArtifacts(fingerprintArtifacts: true, projectName: 'maven-build', selector: lastSuccessful())
        deploy(adapters: [tomcat9(credentialsId: 'tomcat-web', path: '', url: 'http://13.232.126.84:8080')], contextPath: '/newapp', war: '**/*.war')
      }
    }

  }
}
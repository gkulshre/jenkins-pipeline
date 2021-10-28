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
        deploy(adapters: [tomcat9(credentialsId: 'tomcat-web', path: '', url: 'http://13.127.219.52:8080')], contextPath: '/newapp-new', war: '**/*.war')
      }
    }

    stage('Docker Build and Tag') {
      steps {
        sh 'docker build -t samplewebapp:latest .'
        sh 'docker tag samplewebapp gkulshre/samplewebapp:latest'
      }
    }

    stage('Publish image to Docker Hub') {
      steps {
        withDockerRegistry(credentialsId: 'dockerHub') {
          sh 'docker push gkulshre/samplewebapp:latest'
        }

      }
    }

  }
}
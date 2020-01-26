pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs/javadoc/*'
        junit 'build/test-results/test/*.xml'
      }
    }

    stage('Mail Notification') {
      steps {
        mail(subject: 'Build Notification', body: 'Hello', from: 'ga_tadjer@esi.dz', to: 'gn_fekir@esi.dz')
      }
    }

  }
}
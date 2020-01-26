pipeline {
  agent any
  stages {
    stage('Build') {
      post {
        failure {
          script {
            message="failure"
          }

        }

        success {
          script {
            message="Success"
          }

        }

      }
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
        mail(subject: 'Build Notification', body: '${message}', from: 'ga_tadjer@esi.dz', to: 'gn_fekir@esi.dz')
      }
    }

  }
}
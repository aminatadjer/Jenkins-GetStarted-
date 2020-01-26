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
        mail(subject: 'Build Notification', body: "${message}", from: 'ga_tadjer@esi.dz', to: 'gn_fekir@esi.dz')
      }
    }

    stage('Code Analysis') {
      parallel {
        stage('Code Analysis') {
          steps {
            withSonarQubeEnv('sonar') {
              bat 'gradle sonarqube'
            }

          }
        }

        stage('Test Reporting') {
          steps {
            jacoco()
          }
        }

      }
    }

    stage('Deployment') {
      steps {
        bat 'gradle publish'
      }
    }

    stage('slack ') {
      steps {
        slackSend(baseUrl: 'https://hooks.slack.com/services/', teamDomain: 'outils-workspace', token: 'TRQ5TN6LD/BSSUG0EF5/3OyM02whwrisz384YnM9T5ey', message: 'deployee', channel: 'general')
      }
    }

  }
}
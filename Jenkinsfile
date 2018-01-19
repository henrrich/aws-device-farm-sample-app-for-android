pipeline {
  agent any
  stages {
    stage('build') {
      agent any
      steps {
        deleteDir()
        git 'https://github.com/henrrich/aws-device-farm-sample-app-for-android.git'
        sh 'fastlane test'
      }
    }
  }
}
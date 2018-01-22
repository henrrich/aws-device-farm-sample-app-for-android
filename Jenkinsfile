pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        cleanWs()
    git 'https://github.com/henrrich/aws-device-farm-sample-app-for-android.git'
        sh 'fastlane test'
      }
    }
    stage('upload') {
      steps {

        script {

            echo pwd()

            sh 'ls -la'

            sh 'ls -l app/build/outputs/apk/debug'

          def server = Artifactory.newServer url: 'http://localhost:8081/artifactory/', username: 'native', password: 'native'

          def uploadSpec = """{
            "files": [
              {
                "pattern": "app/build/outputs/apk/debug/*.apk",
                "target": "android-snapshot-local/android-demo-app/",
                "props": "status=new_build"
              }
            ]
          }"""
          server.upload(uploadSpec)
        }
        
      }
    }
  }
}
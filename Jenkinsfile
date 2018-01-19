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
    stage('upload') {
      steps {
        script {
          def server = Artifactory.newServer url: 'http://localhost:8081/artifactory/', username: 'native', password: 'native'
          
          def uploadSpec = """{
            "files": [
              {
                "pattern": "*/app/build/outputs/apk/debug/*.apk",
                "target": "android-snapshot-local/android-demo-app/",
                "props": "status=new_build"
              }
            ]
          }"""
          def buildInfo = server.upload(uploadSpec)
          buildInfo.env.capture = true
          
          buildInfo.name = 'android_demo_app'
          buildInfo.number = 'v1.2.3'
          server.publishBuildInfo buildInfo
        }
        
      }
    }
  }
}
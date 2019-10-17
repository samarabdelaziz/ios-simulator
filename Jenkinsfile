pipeline {
    agent {label 'ios'}
     stages {
        stage('PR Check') {
          
          steps{
            sh """
              
              /Applications/Xcode9.4.1.app/Contents/Developer/Applications/Simulator.app/Contents/MacOS/Simulator -CurrentDeviceUDID 7A75398A-DC41-4BEE-85EE-19EE9C2BFAE3
              #xcodebuild -project simulatortest.xcodeproj -scheme simulatortest -archivePath /Users/jenkins/Desktop/Samaripa archive
              #xcodebuild -exportArchive -archivePath /Users/jenkins/Desktop/Samaripa.xcarchive -exportPath  /Users/jenkins/Desktop/ipaoutput -exportOptionsPlist /Users/jenkins/Desktop/ipa.plist

             """
          }
        }
     }
}

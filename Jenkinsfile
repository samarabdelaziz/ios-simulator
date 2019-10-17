pipeline {
    agent {label 'ios'}
     stages {
        stage('build and archive') {
            steps{
            sh """
              
              #/Applications/Xcode9.4.1.app/Contents/Developer/Applications/Simulator.app/Contents/MacOS/Simulator -CurrentDeviceUDID 7A75398A-DC41-4BEE-85EE-19EE9C2BFAE3
              #cd /Users/jenkins/Desktop/simulatortest
              security unlock-keychain -p V0daf0ne_123
              xcodebuild -project simulatortest.xcodeproj -scheme simulatortest -archivePath /Users/jenkins/Desktop/Samaripa archive
              #xcodebuild -exportArchive -archivePath /Users/jenkins/Desktop/Samaripa.xcarchive -exportPath  /Users/jenkins/Desktop/ipaoutput -exportOptionsPlist /Users/jenkins/Desktop/ipa.plist
              #/Applications/Xcode9.4.1.app/Contents/Developer/Applications/Simulator.app/Contents/MacOS/Simulator -CurrentDeviceUDID 7A75398A-DC41-4BEE-85EE-19EE9C2BFAE3
              #xcrun simctl boot 7A75398A-DC41-4BEE-85EE-19EE9C2BFAE3
              #xcrun simctl install 7A75398A-DC41-4BEE-85EE-19EE9C2BFAE3  /Users/jenkins/Desktop/Samaripa.xcarchive/Products/Applications/simulatortest.app
              
             """
          }
        }

        stage('Export IPA') {
            steps{
            sh """
              
              #/Applications/Xcode9.4.1.app/Contents/Developer/Applications/Simulator.app/Contents/MacOS/Simulator -CurrentDeviceUDID 7A75398A-DC41-4BEE-85EE-19EE9C2BFAE3
              #cd /Users/jenkins/Desktop/simulatortest
              #security unlock-keychain -p V0daf0ne_123
              #xcodebuild -project simulatortest.xcodeproj -scheme simulatortest -archivePath /Users/jenkins/Desktop/Samaripa archive
              xcodebuild -exportArchive -archivePath /Users/jenkins/Desktop/Samaripa.xcarchive -exportPath  /Users/jenkins/Desktop/ipaoutput -exportOptionsPlist /Users/jenkins/Desktop/ipa.plist
              #/Applications/Xcode9.4.1.app/Contents/Developer/Applications/Simulator.app/Contents/MacOS/Simulator -CurrentDeviceUDID 7A75398A-DC41-4BEE-85EE-19EE9C2BFAE3
              #xcrun simctl boot 7A75398A-DC41-4BEE-85EE-19EE9C2BFAE3
              #xcrun simctl install 7A75398A-DC41-4BEE-85EE-19EE9C2BFAE3  /Users/jenkins/Desktop/Samaripa.xcarchive/Products/Applications/simulatortest.app
              
             """
          }
        }

        stage('Install app on simulator') {
            steps{
            sh """
              
              #/Applications/Xcode9.4.1.app/Contents/Developer/Applications/Simulator.app/Contents/MacOS/Simulator -CurrentDeviceUDID 7A75398A-DC41-4BEE-85EE-19EE9C2BFAE3
              #cd /Users/jenkins/Desktop/simulatortest
              #security unlock-keychain -p V0daf0ne_123
              #xcodebuild -project simulatortest.xcodeproj -scheme simulatortest -archivePath /Users/jenkins/Desktop/Samaripa archive
              #xcodebuild -exportArchive -archivePath /Users/jenkins/Desktop/Samaripa.xcarchive -exportPath  /Users/jenkins/Desktop/ipaoutput -exportOptionsPlist /Users/jenkins/Desktop/ipa.plist
              #/Applications/Xcode9.4.1.app/Contents/Developer/Applications/Simulator.app/Contents/MacOS/Simulator -CurrentDeviceUDID 7A75398A-DC41-4BEE-85EE-19EE9C2BFAE3
              #xcrun simctl boot 7A75398A-DC41-4BEE-85EE-19EE9C2BFAE3
              xcrun simctl install 7A75398A-DC41-4BEE-85EE-19EE9C2BFAE3  /Users/jenkins/Desktop/Samaripa.xcarchive/Products/Applications/simulatortest.app
              
             """
          }
     }
}
     }


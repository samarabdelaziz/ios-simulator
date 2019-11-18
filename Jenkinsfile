pipeline {
    agent {label 'ios'}
     stages {
        stage('build and archive') {
            steps{
               
            sh """
              
             
              #cd /Users/jenkins/Desktop/simulatortest
               cd /Users/jenkins/Desktop/IOS-Project/SearchBarInTable
              security unlock-keychain -p V0daf0ne_123
              #xcodebuild -project simulatortest.xcodeproj -scheme simulatortest -archivePath /Users/jenkins/Desktop/Samaripa archive
              xcodebuild -project SearchBarInTable.xcodeproj -scheme SearchBarInTable -archivePath /Users/jenkins/Desktop/IOS_Project_Arch archive
             """
          }
        }

        stage('Export IPA') {
            steps{
                 withCredentials([usernamePassword(credentialsId: 'NexusPublisher', passwordVariable: 'nexus_PWD', usernameVariable: 'nexus_USER')]) {
            sh """
              
              

              #xcodebuild -exportArchive -archivePath /Users/jenkins/Desktop/Samaripa.xcarchive -exportPath  /Users/jenkins/Desktop/ipaoutput -exportOptionsPlist /Users/jenkins/Desktop/ipa.plist
              #xcodebuild -exportArchive -archivePath /Users/jenkins/Desktop/IOS_Project_Arch.xcarchive -exportPath  /Users/jenkins/Desktop/IOS_ipaoutput -exportOptionsPlist /Users/jenkins/Library/Developer/Xcode/DerivedData/SearchBarInTable-auxpzfyrvkmkahfqxvcrklignzeu/Info.plist
              xcodebuild -exportArchive -archivePath /Users/jenkins/Desktop/IOS_Project_Arch.xcarchive -exportPath  /Users/jenkins/Desktop/IOS_ipaoutput -exportOptionsPlist /Users/jenkins/Desktop/ipa.plist
              open /Applications/Xcode11.1.app/Contents/Developer/Applications/Simulator.app/Contents/MacOS/Simulator 
             
             """
          }
        }
        }
          stage('Publish to nexus') {
               steps{
                   sh "pwd"
                
                   sh "ls -la /Users/jenkins/Desktop/IOS_ipaoutput"
                   //sh "tar -zcvf IPA_IOS_ipaoutput.tar.gz IOS_ipaoutput/"
                   //sh "rm -rf IPA_IOS_ipaoutput.tar.gz"
                   nexusArtifactUploader(
                        nexusVersion:'nexus3',protocol:'https',
                        
                        nexusUrl:'nexus-vfre.skytap-tss.vodafone.com',
                        groupId:'vf.ios.ipa',
                        version:'v.1',
                        repository: "IOS-simulator",
                        credentialsId:'nexusPublisher',
                        artifacts: [
                            [artifactId:"ios_ipa",
                            file:"Users/jenkins/Desktop/IOS_ipaoutput/SearchBarInTable.ipa",
                            type:'ipa']
                        ]
                ) 
                   
                   
               }
          }

        stage('Install app on simulator') {
            steps{
            sh """
              
              #/Applications/Xcode11.1.app/Contents/Developer/Applications/Simulator.app/Contents/MacOS/Simulator -CurrentDeviceUDID 7A75398A-DC41-4BEE-85EE-19EE9C2BFAE3
              #xcrun simctl boot C6382819-1EA6-4AF6-A3B7-F388A2A94212
              #xcrun simctl install 7A75398A-DC41-4BEE-85EE-19EE9C2BFAE3  /Users/jenkins/Desktop/Samaripa.xcarchive/Products/Applications/simulatortest.app
              #xcrun simctl install C6382819-1EA6-4AF6-A3B7-F388A2A94212  /Users/jenkins/Desktop/Samaripa.xcarchive/Products/Applications/simulatortest.app
               #xcrun simctl install C6382819-1EA6-4AF6-A3B7-F388A2A94212 /Users/jenkins/Library/Developer/Xcode/DerivedData/simulatortest-exbrzxdghrrzyfczpztjkfclkdre/Build/Products/Debug-iphonesimulator/simulatortest.app
               xcrun simctl install C6382819-1EA6-4AF6-A3B7-F388A2A94212 /Users/jenkins/Library/Developer/Xcode/DerivedData/SearchBarInTable-auxpzfyrvkmkahfqxvcrklignzeu/Build/Products/Debug-iphonesimulator/SearchBarInTable.app
            """
          }
     }
         
    
         stage('Launch app on simulator') {
            steps{
            sh """
              
              #xcrun simctl launch C6382819-1EA6-4AF6-A3B7-F388A2A94212 test.simulatortest1
           
             """
          }
     }
         
         
         
}
     }



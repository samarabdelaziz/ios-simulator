pipeline {
    agent {label 'ios'}
     stages {
         
        
         stage('unit testing') {
             steps{
                slackSend (color: '#FFFF00', message: "Unit Testing Started: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
                sh """
                cd /Users/jenkins/Desktop/IOS-Project/SearchBarInTable
                xcodebuild  -scheme SearchBarInTable  -destination 'platform=iOS Simulator,OS=13.1,name=iPhone 11 Pro Max' test > /Users/jenkins/Desktop/IOS_Project/ut_results.txt
                
                """ 
             }
         
            post {
         success {
               slackSend (color: '#00FF00', message: "UT SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
                 }
         failure {
               slackSend (color: '#FF0000', message: "UT FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
                }
             }
         }
         
         
        stage('build and archive') {
            steps{
               
            sh """
              
             
              
               cd /Users/jenkins/Desktop/IOS-Project/SearchBarInTable
              security unlock-keychain -p V0daf0ne_123
              
              xcodebuild -project SearchBarInTable.xcodeproj -scheme SearchBarInTable -archivePath /Users/jenkins/Desktop/IOS_Project_Arch archive
             """
          }
        }

        stage('Export IPA') {
            steps{
                 
            sh """
              
              

              
              xcodebuild -exportArchive -archivePath /Users/jenkins/Desktop/IOS_Project_Arch.xcarchive -exportPath  /Users/jenkins/Desktop/IOS_ipaoutput -exportOptionsPlist /Users/jenkins/Desktop/ipa.plist
              #xcrun simctl boot C6382819-1EA6-4AF6-A3B7-F388A2A94212
              open /Applications/Xcode11.1.app/Contents/Developer/Applications/Simulator.app/Contents/MacOS/Simulator 
              cd /Users/jenkins/Desktop/IOS_ipaoutput
             
             """
          }
        }
        
          stage('Publish to nexus') {
               steps{
                   sh """
                   pwd
                
                   ls -la /Users/jenkins/Desktop/IOS_ipaoutput
                   cd /Users/jenkins/Desktop/IOS_ipaoutput
                    pwd
                   
                   """
                   nexusArtifactUploader(
                        nexusVersion:'nexus3',protocol:'https',
                        
                        nexusUrl:'nexus-vfre.skytap-tss.vodafone.com',
                        groupId:'vf.ios.ipa',
                        version:"v.${env.BUILD_NUMBER}",
                        repository: "IOS-simulator",
                        credentialsId:'NexusPublisher',
                        artifacts: [
                            [artifactId:"ios_ipa",
                            file:"/Users/jenkins/Desktop/IOS_ipaoutput/SearchBarInTable.ipa",
                            type:'ipa']
                        ]
                ) 
                   
                   
               }
          }

        stage('Install app on simulator') {
            steps{
            sh """
              
              
              #xcrun simctl boot C6382819-1EA6-4AF6-A3B7-F388A2A94212
             
               xcrun simctl install C6382819-1EA6-4AF6-A3B7-F388A2A94212 /Users/jenkins/Library/Developer/Xcode/DerivedData/SearchBarInTable-auxpzfyrvkmkahfqxvcrklignzeu/Build/Products/Debug-iphonesimulator/SearchBarInTable.app
            """
          }
     }
         
    
         stage('Launch app on simulator') {
            steps{
            sh """
              
              xcrun simctl launch C6382819-1EA6-4AF6-A3B7-F388A2A94212 SearchBarInTable1
           
             """
          }
     }
         
       
   


         
         
         
}
     }



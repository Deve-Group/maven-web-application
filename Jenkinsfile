node{
    
properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '5', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), pipelineTriggers([pollSCM('* * * * *')])])

def MavenHome = tool name: "Maven 3.9.6"

echo "The Job name is: ${JOB_NAME} " 
echo "The Node name is:  ${NODE_NAME}"
echo "The Build Number is:  ${BUILD_NUMBER}"
//echo "Jenkins Home path is: ${JENKINS_HOME}"

try{
stage('CheckoutCode'){
git credentialsId: '1d892077-c906-4800-aeca-573f4652fa84', url: 'https://github.com/Deve-Group/maven-web-application.git'
}
stage('BuildTheCode'){
sh "${MavenHome}/bin/mvn clean package"
}
/*
stage('BuildToSonarQube'){
sh "${MavenHome}/bin/mvn sonar:sonar"
}
stage('DiployCode'){
sh "${MavenHome}/bin/mvn sonar:sonar deploy"
}

*/
}//try closing
catch (e) {
    // If there was an exception thrown, the build failed
    currentBuild.result = "FAILED"
}//catch closing
finally {
    // Success or failure, always send notifications
    sendlocknotifications(currentBuild.result)
}//finall closing
    
}//node closing

def sendslacknotification(String buildStatus = 'STARTED') {
  // build status of null means successful
  buildStatus =  buildStatus ?: 'SUCCESSFUL'

  // Default values
  def colorName = 'RED'
  def colorCode = '#FF0000'
  def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
  def summary = "${subject} (${env.BUILD_URL})"

  // Override default values based on build status
  if (buildStatus == 'STARTED') {
    colorName = 'YELLOW'
    colorCode = '#FFFF00'
  } else if (buildStatus == 'SUCCESSFUL') {
    colorName = 'GREEN'
    colorCode = '#00FF00'
  } else {
    colorName = 'RED'
    colorCode = '#FF0000'
  }

  // Send notifications
  slackSend (color: colorCode, message: summary)
}

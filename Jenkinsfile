node{

echo "Buil Number: ${env.BUILD_NUMBER}"
echo "Jon name is: ${env.JOB_NAME}"
echo "Node name is: ${env.NODE_NAME}"

def MavenHome = tool name: "Maven 3.9.6"

properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '5', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), pipelineTriggers([pollSCM('* * * * *')])])

stage('CheckoutCode'){
git credentialsId: '1d892077-c906-4800-aeca-573f4652fa84', url: 'https://github.com/Deve-Group/maven-web-application.git'
}

stage('BuildCode'){
sh "${MavenHome}/bin/mvn clean package"
}

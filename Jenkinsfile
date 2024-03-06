node{
    
properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '5', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), pipelineTriggers([pollSCM('* * * * *')])])

def MavenHome = tool name: "Maven 3.9.6"

echo "The Job name is: ${env.JOB_NAME} " 
echo "The Node name is:  ${env.NODE_NAME}"
echo "The Build Number is:  ${env.BUILD_NUMBER}"
//echo "Jenkins Home path is: ${env.JENKINS_HOME}"


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

}

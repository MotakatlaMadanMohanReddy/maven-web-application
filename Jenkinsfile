def sendslacknitification(String buildStatus = 'STARTED') {
  // build status of null means successful
  buildStatus =  buildStatus ?: 'SUCCESS'

  // Default values
  def colorName = 'RED'
  def colorCode = '#FF0000'
  def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
  def summary = "${subject} (${env.BUILD_URL})"

  // Override default values based on build status
  if (buildStatus == 'STARTED') {
    color = 'YELLOW'
    colorCode = '#FFFF00'
  } else if (buildStatus == 'SUCCESS') {
    color = 'GREEN'
    colorCode = '#00FF00'
  } else {
    color = 'RED'
    colorCode = '#FF0000'
  }

  // Send notifications
  slackSend (color: colorCode, message: summary)
}





node{

echo"node name is : ${env.JOB_NAME}"
echo"job name is : ${env.NODE_NAME}"
properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '5', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])
 def mavenhome= tool name: 'maven3.8.4'
  try{
//get the code from Github repo
stage('checkoutcode')
{
git branch: 'development', credentialsId: '910389fb-ae6f-4007-aa3d-200d0ca5ff2f', url: 'https://github.com/MotakatlaMadanMohanReddy/maven-web-application.git'
}
//Do the build using maven build tool
stage('Build')
{
sh "${mavenhome}/bin/mvn clean package"
}
/*
//execute sonarqube report
 stage('executesonarQubeReport')
 {
 sh "${mavenhome}/bin/mvn sonar:sonar"
 }
 
 //upload artifacts into artifacts repo
 stage('Upload articats into nexus')
 {
 sh "${mavenhome}/bin/mvn deploy"
 }
 
 //deply the applicatio in tomcat server
 stage('Deployapplicatiojnintotomcatserver')
 {
 sshagent(['5e72bf45-5661-4c12-b708-8f8b16f93307']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.235.48.186:/opt/apache-tomcat-9.0.62/webapps/"
}
}
*/
}//try closing
  catch(e){
     currentBuild.result = "FAILED"
  }
  finally{
    sendslacknitification(currentBuild.result)
  }
}

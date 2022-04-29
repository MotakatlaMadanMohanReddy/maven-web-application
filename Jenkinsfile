node{

echo"node name is : ${env.JOB_NAME}"
echo"job name is : ${env.NODE_NAME}"

 def mavenhome= tool name: 'maven3.8.4'
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
}

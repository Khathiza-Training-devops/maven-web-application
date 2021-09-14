node ('master')
 {
  
  def mavenHome = tool name: "maven3.8.2"
  
      echo "GitHub BranhName ${env.BRANCH_NAME}"
      echo "Jenkins Job Number ${env.BUILD_NUMBER}"
      echo "Jenkins Node Name ${env.NODE_NAME}"
  
      echo "Jenkins Home ${env.JENKINS_HOME}"
      echo "Jenkins URL ${env.JENKINS_URL}"
      echo "JOB Name ${env.JOB_NAME}"
  
   //properties([[$class: 'JiraProjectProperty'], buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '2', daysToKeepStr: '', numToKeepStr: '2')), pipelineTriggers([pollSCM('* * * * *')])])
  
  timestamps {   // TO DISPLAY TIMESTAMP IN CONSOLE OUTPUT
    stage('CheckoutCode')
    {
        git credentialsId: '51a8a1f1-5849-40d5-a5ab-9159f1082b6e', url: 'https://github.com/Khathiza-Training-devops/maven-web-application.git'
    }
    stage('Build')
    {
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage('SonarQubeReport')
    {
        sh "${mavenHome}/bin/mvn clean package sonar:sonar"
    }
     stage('UploadArtifact')
    {
        sh "${mavenHome}/bin/mvn clean deploy"
    }
    stage('DeployinTomcat')
    {
        sshagent(['tomcatcredentials_new']) {
    sh "scp -o strictHostKeyChecking=no target/*.war ec2-user@52.66.129.57:/opt/apache-tomcat-9.0.52/webapps/NewWar.war" 
    }
    }
    }
 
 stage('EmailNotification')
 {
 mail bcc: 'khathizasa@gmail.com', body: '''Build is over

 Thanks,
 Mithun Technologies,
 9980923226.''', cc: 'khathizasu@gmail.com', from: '', replyTo: '', subject: 'Build is over!!', to: 'abdullathif36@gmail.com'
 }
 */
 
 }

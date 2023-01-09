node
{
 def mavenHome = tool name: "maven3.8.6" 
  stage('CheckoutCode')
  {
   git credentialsId: '6d6b2404-741e-42cf-ba12-dac86af8df64', url: 'https://github.com/Bluewash/maven-web-application.git'
  } 
  stage('Build')
  {
   sh "${mavenHome}/bin/mvn clean package"  
  } 
  stage('ExecuteSonarQubeReport')
  {
   sh "${mavenHome}/bin/mvn sonar:sonar"  
  }
  stage('UploadArtifactIntoNexus')
  {
   sh "${mavenHome}/bin/mvn deploy" 	
  }
  stage('DeployApplicationIntoTomcat') 
  {
  sshagent(['6caf5fb3-adc9-4ee9-a3ad-822313ae339f']) 
  {
   sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@100.27.3.200:/opt/apache-tomcat-9.0.70/webapps/"
  }
  }
}

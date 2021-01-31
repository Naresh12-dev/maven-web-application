 node('nodes')
 {
     
     def mavenHome = tool name: "maven3.6.3"
     
    stage('CheckoutCode')
    {
     git branch: 'development', credentialsId: '957b9901-8ee2-41b2-88cd-33948f46f4d9', url: 'https://github.com/Naresh12-dev/maven-web-application.git'   
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
    
    stage('DeployApplicationIntoTomcatServer')
    {
        sshagent(['80ebad91-1e0d-4f18-a30b-7b85bedb5d6a']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.233.110.21://opt/apache-tomcat-9.0.41/webapps/"
        }
    }
    
}

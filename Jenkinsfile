env.dockerimagename="devopsbasservice/buildonframework:buildon-v1.0"
node {
  stage ('Banking_Checkout') {
   //If some other Repository is to be given apart from current repo, provide git URL as below.
    checkout scm
  }
   stage ('Banking_Build') {
    sh 'mvn clean package -DskipTests=True'
  }
  stage ('Banking_UnitTest') {
    sh 'mvn test'
  }
   stage ('Banking_CodeAnalysis') {
    sh 'mvn sonar:sonar -Dmaven.test.failure.ignore=true -DskipTests=true -Dsonar.sources=src/main/java'
   }

   stage ('Banking_NexusUpload') {
   
          sh "mvn deploy -DskipTests=true"
   }
  
   stage ('Banking_tomcatDeployment') {
    sh 'mvn -P tomcatDeployment tomcat7:redeploy -DskipTests'
   }   
}    

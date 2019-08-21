node{
      def mvnHome = tool name: 'maven 3.5.4', type: 'maven' 
      stage('Checkout'){
         git 'https://github.com/rupanisantosh/java-tomcat-maven-example.git'
       
      }  
      stage('Build'){
         //// Get maven home path and build
        sh "${mvnHome}/bin/mvn clean package -Dmaven.test.skip=true"
      }
     stage ('Test-JUnit'){
         sh "'${mvnHome}/bin/mvn' test surefire-report:report"
      }  
    
      stage('Deploy') {     
            sshagent(['Tomcat-jenkins-SSH']) {
                   echo "JENKINS_URL"
               //sh 'scp -o StrictHostKeyChecking=no target/tomcatdeploymnetdemo.war jenkins@34.236.124.22:/opt/tomcat/webapps'
                  sh 'scp -o StrictHostKeyChecking=no target/*.war jenkins@34.236.124.22:/opt/apache-tomcat-8.5.43/webapps'
              
          }
         
     }
      
 }

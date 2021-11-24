node{
 stage('scm checkout')
  {
   git 'https://github.com/ybsgit/my-app' 
  }
  stage('Compile-package')
  {
    sh 'mvn package'
  }
 stage('SonarQube Analysis')
 {
  withSonarQubeEnv('sonar-vprofile') {
   sh 'mvn sonar:sonar'
}
 }
       stage("Quality Gate"){
          timeout(time: 1, unit: 'HOURS') {
              def qg = waitForQualityGate()
              if (qg.status != 'OK') {
                  error "Pipeline aborted due to quality gate failure: ${qg.status}"
              }
          }
      }   
 
 stage('Deploy to tomcat')
 {
  sshagent(['tomcat-new']) {
    sh 'scp -o StrictHostKeyChecking=no scp target/*.war root@10.182.0.36:/var/lib/tomcat9/webapps/'
}
 }
}

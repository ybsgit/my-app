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
}

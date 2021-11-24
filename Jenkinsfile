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
    mvn sonar:sonar
}
 }
}

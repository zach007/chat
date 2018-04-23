node {
   def mvnHome
   stage('checkout') {
      git 'git@github.com:zach007/Chat.git'
      echo 'check out from git@github.com:zach007/Chat.git'
      mvnHome = tool 'maven_3.5'
   }

  stage('SonarQube analysis') {
    withSonarQubeEnv('http://192.168.0.103:9000') {
      // requires SonarQube Scanner for Maven 3.2+
      cd
      sh 'mvn clean verify sonar:sonar'
      sh 'mvn clean install'
      sh 'mvn sonar:sonar'
    }
  }

   stage('building') {
      if (isUnix()) {
         echo 'maven building in Linux'
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         echo 'maven building in Windows'
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
}
node {
    env.JAVA_HOME="${tool 'java-jdk1.8.0_131-32'}"
    env.PATH="${env.JAVA_HOME}/bin:${env.PATH}"
   def mvnHome
    mvnHome = tool 'apache-maven-3.2.3'
   stage('Down code') {
      git 'https://github.com/freemanlingli/hello.git'
     
   }
   stage('Run test') {
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn'  test "
      } else {
         bat(/"${mvnHome}\bin\mvn" test /)
      }
   }   
   stage('Package') {
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('archive') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.jar'
   }
}
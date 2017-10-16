node {
    env.JAVA_HOME="${tool 'java-jdk1.8.0_131-32'}"
    env.PATH="${env.JAVA_HOME}/bin:${env.PATH}"
   def mvnHome
    mvnHome = tool 'apache-maven-3.2.3'
   stage('下载git代码') {
      git 'https://github.com/freemanlingli/hello.git'
     
   }
   stage('测试') {
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn'  test "
      } else {
         bat(/"${mvnHome}\bin\mvn" test /)
      }
   }   
   stage('打包') {
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('归档') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.jar'
   }
}
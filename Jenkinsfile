pipeline { 

  agent any
  
  tools{
    maven "Maven3"
    jdk "JDK 9.0.4"
    
  }
  
  stages {
    stage("cloning"){
      steps{
        echo 'cloning main branch'
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'gitToken', url: 'https://github.com/FDator/Case-Study-for-CI-.git']]])
      }
    }
    stage("build"){
      steps{
        sh 'mvn verify'
        
        echo 'setting up junit'
        sh 'cd src/main/java/org/psnbtech/ ; javac -cp "../lib/junit-platform-console-standalone-1.7.0-all.jar" GameTest.java'
        
        echo 'building the application'
        sh "mvn --version"
        sh "mvn clean compile"
      }
    }
      stage("testing"){
      steps{
        echo 'running junit tests'
          sh 'cd src/ ; java -jar ../lib/junit-platform-console-standalone-1.7.0-all.jar -cp "." --select-class GameTest --reports-dir="reports"'
          junit 'src/reports/*-jupiter.xml'
      }
    }
}
}

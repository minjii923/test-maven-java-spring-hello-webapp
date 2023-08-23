pipeline {
  agent any

  triggers {
    pollSCM('* * * * *')
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', 
        url: 'https://github.com/minjii923/test-maven-java-spring-hello-webapp/blob/main/pipeline'
      }
    }
    stage('Build') {
      steps {
        sh 'mvn clean package -DskipTests'
      }
    }
    stage('Test') {
      steps {
        sh 'mvn test'
      }
    }
    stage('Deploy') {
      steps {
        deploy adapters: [tomcat9(credentialsId: 'tomcat-manager', url: 'http://192.168.56.103:8080/')], contextPath: null, war: 'target/hello-world.war'
      }
    }
  }
}

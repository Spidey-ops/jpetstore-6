pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'first jenkins pipeline'
        sh './mvnw clean compile'
      }
    }

    stage('Unit Test') {
      steps {
        sh './mvnw test'
        junit '**/target/surefire-reports/TEST-*.xml'
      }
    }

    stage('Static Analysis') {
      steps {
        sh '''./mvnw sonar:sonar \\
  -Dsonar.projectKey=JPetstore \\
  -Dsonar.host.url=http://3.110.231.173:9000 \\
  -Dsonar.login=sqp_03cd56f0666ec629b5a11f4a3c2270439082db69'''
      }
    }

    stage('Package') {
      steps {
        sh '''./mvnw package -DskipTests=true
'''
      }
    }

    stage('Integration Test') {
      steps {
        node(label: 'test') {
          sh '''./mvnw verify -P tomcat90
'''
        }

      }
    }

  }
}
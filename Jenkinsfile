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
  -Dsonar.projectKey=Jpetstore \\
  -Dsonar.host.url=http://15.206.2.92:9000 \\
  -Dsonar.login=sqp_3d83ad5200b9d0bde14f713e86601dd7e4df0f6e'''
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
          sh '''./mvn verify -P tomcat90
'''
        }

      }
    }

  }
}
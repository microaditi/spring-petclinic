pipeline {
  agent {
    node {
      label 'test'
    }

  }
  stages {
    stage('compile') {
      steps {
        sh './mvnw clean compile'
      }
    }

    stage('Static Analysis') {
      steps {
        sh '''./mvnw sonar:sonar \\
-Dsonar.host.url=http://172.31.29.33:9000/ \\
-Dsonar.projectKey=Petclinic \\
-Dsonar.login=sqp_1472fd2453bb54261a12845425e00587c55c1113'''
      }
    }

    stage('Unit Test') {
      steps {
        sh './mvnw "-Dtest=**/petclinic/*/*.java" test'
      }
    }

    stage('Package') {
      steps {
        sh './mvnw package -DskipTests=true'
      }
    }

    stage('Deploy') {
      parallel {
        stage('Deploy') {
          steps {
            sh '''./mvnw spring-boot:run </dev/null &>/dev/null &
'''
          }
        }

        stage('Integration and Performance Tests') {
          steps {
            sh './mvnw verify'
            junit '**/target/surefire-reports/*.xml'
            perfReport '**/target/jmeter/results/*'
          }
        }

      }
    }

  }
}
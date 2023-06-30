pipeline {
  agent any
  stages {
    stage('compile') {
      steps {
        sh './mvnw clean compile'
      }
    }

    stage('Static Analysis') {
      steps {
        sh '''./mvn clean verify sonar:sonar \\
  -Dsonar.projectKey=Petclinic/ \\
  -Dsonar.projectName=\'Petclinic\'/ \\
  -Dsonar.host.url=http://3.110.75.182:9000/ \\
  -Dsonar.token=sqp_f5478bae7d9e859f4a5396350144dc931f8cc198'''
      }
    }

  }
}
pipeline {
  agent any
  tools {
    gradle 'Gradle'
  }
  stages {
    stage('Git checkout') {
      steps {
        git branch: 'master', url: 'https://github.com/kekadiri/gradle-example.git'
      }
    }
    stage('build') {
      steps {
        sh 'gradle clean build'
      }
    }
    stage('Sonar Quality checks') {
      steps {
        script {
        withSonarQubeEnv(credentialsId: 'sonarqube') {
        sh 'gradle sonarqube'
      }
    }
      }
    }
  }
}
      

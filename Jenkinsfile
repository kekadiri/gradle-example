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
    stage('Deploy to Nexus') {
            steps {
               withCredentials([usernamePassword(credentialsId: 'nexus-Repo', usernameVariable: 'admin', passwordVariable: 'password')]) {
                    script {
                        // Deploy artifacts to Nexus
                       sh 'gradle publish' 
                    }
                }
            }
        }
    }
  }
}
      

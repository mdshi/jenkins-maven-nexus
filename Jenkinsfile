pipeline {
    agent any
    tools { 
        maven 'M3' 
        jdk 'Java' 
    }
    stages {
    stage ('Initialize') {
      steps {
        sh '''
          echo "PATH = ${PATH}"
          echo "M2_HOME = ${M2_HOME}"
        '''
      }
    }
    stage ('Build') {
      steps {
        sh 'mvn clean package'
      }
    }
    stage ('Deploy') {
      when {
        branch 'master'
      }
      steps {
        script {
          currentBuild.displayName = "${REVISION}"
        }
        sh 'mvn deploy scm:tag -Drevision=${REVISION}'
      }
    }
  }
} 
pipeline {
  agent any

  tools {
        maven 'M3915'
    }
  
  stages {
    stage('Build') {
      steps {
        sh "echo Sleep-Time - ${params.SLEEP_TIME}, Port - ${params.APP_PORT}, Branch - ${params.BRANCH_NAME}"
        sh 'mvn clean package -DskipTests=true'
        archiveArtifacts 'target/hello-demo-*.jar'
      }
    }

    stage('Test') {
      steps {
        sh 'mvn test'
        junit(testResults: 'target/surefire-reports/TEST-*.xml', keepProperties: true, keepTestNames: true)
      }
    }
    
    stage('Containerization') {
      steps {
        sh 'echo Docker Build Image..'
        sh 'echo Docker Tag Image....'
        sh 'echo Docker Push Image......'
      }
    }

    stage('Kubernetes Deployment') {
      steps {
        sh 'echo Deploy to Kubernetes using ArgoCD'
      }
    }
    
    stage('Integration Testing') {
      steps {
        sh "sleep ${params.SLEEP_TIME}"
        sh 'echo Testing using cURL commands......'
      }
    }
  }
}

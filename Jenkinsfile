pipeline {
  environment {
    registry = "faroukhajjej1/projet-devops"
    registryCredential = 'dckr_pat_VVIpmnatR2f0aNGVai7aTJ3TfSM' // ID credential Docker dans Jenkins
    dockerImage = ''
    NODE_VERSION = "20.0.0" // ou autre version Node installée dans Jenkins NodeJS plugin
  }
  agent any

  stages {
    stage('Get Code from GitHub') {
      steps {
        echo 'Pulling code...'
        git branch: 'main', url: 'https://github.com/farouk-hajjej/Devops-Projet-5SE1.git'
      }
    }

    stage('Date') {
      steps {
        script {
          echo "Build date: ${new Date().format('MM/dd/yyyy')}"
        }
      }
    }

    stage('Install dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Run tests') {
      steps {
        sh 'npm test' // adapte selon ton script test (jest, mocha, etc.)
      }
      post {
        always {
          junit '**/test-results/*.xml' // si tu génères des rapports JUnit
        }
      }
    }

    stage('Build') {
      steps {
        sh 'npm run build' // build React ou NestJS
      }
    }

    stage('Docker Build') {
      steps {
        script {
          dockerImage = docker.build("${registry}:${env.BUILD_NUMBER}")
        }
      }
    }

    stage('Docker Login') {
      steps {
        script {
          docker.withRegistry('', registryCredential) {
            echo 'Logged in to Docker registry'
          }
        }
      }
    }

    stage('Docker Push') {
      steps {
        script {
          dockerImage.push()
        }
      }
    }

    stage('Cleanup') {
      steps {
        sh "docker rmi ${registry}:${env.BUILD_NUMBER}"
      }
    }

    stage('Docker Compose Deploy') {
      steps {
        sh 'docker-compose up -d --build'
      }
    }
  }

  post {
    success {
      mail to: "hajjej.farouk6@gmail.com",
           from: "jenkins@example.com",
           subject: "SUCCESS: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
           body: "Build succeeded!\nVoir les détails: ${env.BUILD_URL}"
    }
    failure {
      mail to: "hajjej.farouk6@gmail.com",
           from: "jenkins@example.com",
           subject: "FAILURE: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
           body: "Build failed!\nVoir les détails: ${env.BUILD_URL}"
    }
  }
}

pipeline {
  agent any

  tools {
    nodejs "${NODE_VERSION}" // Le nom défini dans "Manage Jenkins > Global Tool Configuration"
  }

  environment {
    registry = "faroukhajjej1/projet-devops"
    registryCredential = 'dckr_pat_VVIpmnatR2f0aNGVai7aTJ3TfSM' // ID des credentials DockerHub dans Jenkins
    dockerImage = ''
    NODE_VERSION = "node-20" // nom exact configuré dans Jenkins (pas un numéro de version !)
  }

  stages {
    stage('Get Code from GitHub') {
      steps {
        echo '📦 Clonage du dépôt Git...'
        git branch: 'main', url: 'https://github.com/farouk-hajjej/Github-Actions-DevOps-Project.git'
      }
    }

    stage('Date') {
      steps {
        script {
          echo "📅 Date de build : ${new Date().format('MM/dd/yyyy')}"
        }
      }
    }

    stage('Install dependencies') {
      steps {
        echo '📥 Installation des dépendances...'
        sh 'npm install'
      }
    }

    stage('Run tests') {
      steps {
        echo '✅ Lancement des tests...'
        sh 'npm test' // adapte à ton projet (ex: jest, mocha, etc.)
      }
      post {
        always {
          junit '**/test-results/*.xml' // facultatif si tu as des rapports JUnit
        }
      }
    }

    stage('Build') {
      steps {
        echo '⚙️ Build de l\'application...'
        sh 'npm run build'
      }
    }

    stage('Docker Build') {
      steps {
        script {
          echo '🐳 Construction de l\'image Docker...'
          dockerImage = docker.build("${registry}:${env.BUILD_NUMBER}")
        }
      }
    }

    stage('Docker Login') {
      steps {
        script {
          echo '🔐 Connexion à DockerHub...'
          docker.withRegistry('', registryCredential) {
            echo 'Connecté à DockerHub'
          }
        }
      }
    }

    stage('Docker Push') {
      steps {
        script {
          echo '🚀 Push de l\'image Docker...'
          dockerImage.push()
        }
      }
    }

    stage('Cleanup') {
      steps {
        echo '🧹 Nettoyage de l\'image locale...'
        sh "docker rmi ${registry}:${env.BUILD_NUMBER} || true"
      }
    }

    stage('Docker Compose Deploy') {
      steps {
        echo '📦 Déploiement avec docker-compose...'
        sh 'docker-compose up -d --build'
      }
    }
  }

  post {
    success {
      mail to: "hajjej.farouk6@gmail.com",
           from: "jenkins@example.com",
           subject: "✅ SUCCESS: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
           body: "Build succeeded!\nVoir les détails ici : ${env.BUILD_URL}"
    }
    failure {
      mail to: "hajjej.farouk6@gmail.com",
           from: "jenkins@example.com",
           subject: "❌ FAILURE: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
           body: "Build failed!\nVoir les détails ici : ${env.BUILD_URL}"
    }
  }
}

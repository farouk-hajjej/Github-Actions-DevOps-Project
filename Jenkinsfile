pipeline {
  agent any

  environment {
    NODE_VERSION = "node-20" // Doit être défini dans "Manage Jenkins > Global Tool Configuration"
    registry = "faroukhajjej1/projet-devops"
    registryCredential = 'dckr_pat_VVIpmnatR2f0aNGVai7aTJ3TfSM' // ID Jenkins pour DockerHub
    dockerImage = ''
  }

  tools {
    nodejs "${NODE_VERSION}"
  }

  triggers {
    githubPush() // Déclenche automatiquement à chaque push GitHub
  }

  stages {

    stage('Récupération du code') {
      steps {
        echo '📦 Clonage du dépôt Git...'
        git branch: 'main', url: 'https://github.com/farouk-hajjej/Github-Actions-DevOps-Project.git'
      }
    }

    stage('Afficher la date') {
      steps {
        script {
          echo "📅 Date de build : ${new Date().format('MM/dd/yyyy HH:mm:ss')}"
        }
      }
    }

    stage('Installation des dépendances') {
      steps {
        echo '📥 Installation des dépendances Node.js...'
        sh 'npm install'
      }
    }

    stage('Tests unitaires') {
      steps {
        echo '✅ Lancement des tests...'
        sh 'npm test'
      }
      post {
        always {
          junit '**/test-results/*.xml' // Optionnel, pour rapports de test
        }
      }
    }

    stage('Build de l\'application') {
      steps {
        echo '⚙️ Build en cours...'
        sh 'npm run build'
      }
    }

    stage('Construction Docker') {
      steps {
        script {
          echo '🐳 Construction de l\'image Docker...'
          dockerImage = docker.build("${registry}:${env.BUILD_NUMBER}")
        }
      }
    }

    stage('Connexion à DockerHub') {
      steps {
        script {
          echo '🔐 Connexion à DockerHub...'
          docker.withRegistry('', registryCredential) {
            echo '✅ Connecté avec succès'
          }
        }
      }
    }

    stage('Push Docker') {
      steps {
        script {
          echo '🚀 Push de l\'image vers DockerHub...'
          docker.withRegistry('', registryCredential) {
            dockerImage.push()
          }
        }
      }
    }

    stage('Nettoyage Docker local') {
      steps {
        echo '🧹 Suppression de l\'image locale...'
        sh "docker rmi ${registry}:${env.BUILD_NUMBER} || true"
      }
    }

    stage('Déploiement via Docker Compose') {
      steps {
        echo '📦 Déploiement avec Docker Compose...'
        sh 'docker-compose up -d --build'
      }
    }
  }

  post {
    success {
      mail to: "hajjej.farouk6@gmail.com",
           from: "jenkins@example.com",
           subject: "✅ SUCCESS: Job ${env.JOB_NAME} #${env.BUILD_NUMBER}",
           body: "Le build a réussi.\nVoir les détails : ${env.BUILD_URL}"
    }
    failure {
      mail to: "hajjej.farouk6@gmail.com",
           from: "jenkins@example.com",
           subject: "❌ FAILURE: Job ${env.JOB_NAME} #${env.BUILD_NUMBER}",
           body: "Le build a échoué.\nVoir les détails : ${env.BUILD_URL}"
    }
  }
}

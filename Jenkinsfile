pipeline {
    agent any

    environment {
        NODE_VERSION = "node-20"
        registry = "faroukhajjej1/projet-devops-test"
        registryCredential = 'dckr_pat_VVIpmnatR2f0aNGVai7aTJ3TfSM'
        dockerImage = ''
    }
    tools {
    nodejs "${NODE_VERSION}"
  }

    stages {
        stage('Get Code from GitHub') {
            steps {
                echo 'Pulling .....'
                git branch: 'main',
                    url: 'https://github.com/farouk-hajjej/Github-Actions-DevOps-Project.git'
            }
        }

        stage('Date') {
            steps {
                script {
                    def date = new Date()
                    def sdf = new java.text.SimpleDateFormat("MM/dd/yyyy")
                    println(sdf.format(date))
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Running npm install...'
                sh 'npm install'
            }
        }
    }
}

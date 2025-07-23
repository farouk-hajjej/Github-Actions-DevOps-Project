pipeline {
environment {
        registry = "faroukhajjej1/projet-devops-test"
        registryCredential = 'dckr_pat_VVIpmnatR2f0aNGVai7aTJ3TfSM'
        dockerImage = ''
    }   
agent any
stages {
    stage('Get Code from GitHub') {
        steps {
            echo 'Pulling .....';
            git branch : 'main',
            url : 'https://github.com/farouk-hajjej/Github-Actions-DevOps-Project.git'
               }
    }
    stage('Date') {
                          steps {
                               script{
                               def date = new Date()
                               sdf = new SimpleDateFormat("MM/dd/yyyy")
                               println(sdf.format(date))
                                       }

                                 }
    }
}

pipeline{
    agent any 

    stages{
        stage("Cloning from Github ..."){
            steps{
                script{
                    echo 'Cloning from Github...'
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], 
                    userRemoteConfigs: [[credentialsId: 'github-token-anime',
                     url: 'https://github.com/Katla-Adithya/anime-recommandation.git']])
                }
            }
        }
    }
}
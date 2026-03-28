pipeline{
    agent any 

    environment{
        VENV_DIR = 'venv'
    }

    stages{stage("Cloning from Github ..."){
            steps{
                script{
                    echo 'Cloning from Github...'
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], 
                    userRemoteConfigs: [[credentialsId: 'github-token-anime',
                    url: 'https://github.com/Katla-Adithya/anime-recommandation.git']])
                }
            }
        }
        stage("making a virtual environment ..."){
            steps{
                script{
                    echo 'Making a virtual environment...'
                    sh '''
                    python -m venv ${VENV_DIR}
                    . ${VENV_DIR}/bin/activate
                    pip install --upgrade pip 
                    pip install -e .
                    pip install dvc
                    '''
                    
                }
            }
        }

        stage('DVC Pull'){
            steps{
                withCredentials([file(credentialsId:'gcp-key-anime', variable :'GOOGLE_APPLICATION_CREDENTIALS')]){
                    script{
                        echo 'DVC Pull....'
                        sh '''
                        . ${VENV_DIR}/bin/activate
                        dvc pull
                        '''
                    }

                }
            }
        }
        
    }
}
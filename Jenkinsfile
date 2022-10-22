pipeline{
    agent { label 'PYHON'}
    stages{
        stage('GIT'){
            steps{
                git branch: 'master' , url: ' https://github.com/mallojuashok/python-webcount.git'
            }
        }
        stage('Python'){
            steps{
                """ sudo apt install python3-pip -y 
                    python -m pip install --upgrade pip
                    pip install -r requirements.txt
                    pip install pytest pytest-azurepipelines
                    pip install tox
                    tox """
            }
        }
        stage('archive results'){
            steps{
                junit '**/junit-py39.xml/*.xml'
            }
        }
        stage('artifacts'){
            steps{
                archiveArtifacts artifacts: '**/webcount-0.1.zip'
            }
        }

    }
}
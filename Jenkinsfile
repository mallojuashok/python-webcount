pipeline{
    agent { label 'PYHON'}
    stages{
        stage('Python'){
            steps{
                sh 'sudo apt install python3-pip -y'
            }
        }
        stage('GIT'){
            steps{
                git branch 'master' , url ' https://github.com/mallojuashok/python-webcount.git'
            }
        }
        stage('PIP3'){
            steps{
                sh 'pip3 install -r requirements.txt'
            }
        }
        stage('TOX'){
            steps{
                sh 'sudo apt install tox'
            }
        }
        stage('Run Tox'){
            steps{
                sh 'tox'
            }
        }
        stage('archive results'){
            steps{
                junit '**/junit-py39.xml/*.xml'
            }
        }
        stage('artifacts'){
            steps{
                archiveArtifacts artifacts '**/webcount-0.1.zip'
            }
        }

    }
}
pipeline {
    agent { label 'PYHON' }
    parameters {
        string(name: 'MAVEN_GOAL', defaultValue: 'tox', description: 'maven goal')

    }
    stages{
        stage('VCS'){
            steps{
                git branch:'master' , url:'https://github.com/mallojuashok/python-webcount.git'
            }
        }
        stage ('Artifactory configuration') {
            steps {
                
                rtMavenDeployer (
                    id: "PYTHON_DEPLOYER",
                    serverId: "My_Frog",
                    releaseRepo: 'askpip-pypi-local',
                    snapshotRepo: 'askpip-pypi-remote'
                )


            }
        }
        stage ('Exec Python') {
            steps {
                rtMavenRun (
                    tool: 'MVN_DFT', // Tool name from Jenkins configuration
                    pom: 'py39.xml',
                    goals: 'tox',
                    deployerId: "PYTHON_DEPLOYER"
                )
            }
        }

        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "My_Frog"
                )
            }
        }


    }
}
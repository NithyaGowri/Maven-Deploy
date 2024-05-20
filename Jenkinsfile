pipeline {
    agent any
    stages {
        stage("Clean Up"){
            steps {
                deleteDir()
            }
        }
        stage("Build"){
            steps {
                dir("Maven-Deploy")
                {
                    powershell 'mvn clean deploy'
                }
                
            }
        }
        
    }
}

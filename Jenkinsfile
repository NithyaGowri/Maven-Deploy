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
                
                    powershell 'mvn clean deploy'
                
            }
        }
        
    }
}

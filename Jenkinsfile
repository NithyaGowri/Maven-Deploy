pipeline {
    agent any
     environment
    {
        PATH = "/E/Maven/apache-maven-3.9.6/bin:$PATH"
        def sonarHome = tool 'jenkins-sonar-scanner-tool'
        def registry = 'https://nithyawipro.jfrog.io'
    }
    stages {
        stage("Clean Up"){
            steps {
                echo "################ CLEAR WORKSPACE ###################"
                deleteDir()
            }
        }
        stage("Build"){
            steps {
                
                    echo "######################## Maven Deployment ########################"
                    powershell 'mvn clean --file *.pom'
                
                
            }
        }
        stage('JFrog Integration')
        {
            steps
            {
                echo "#####################JFrog Artifact Upload######################"
                
                script
                {
                    def server = Artifactory.newServer url:registry+"/artifactory" , credentialsId:"jfrogInteg"
                    def properties = "buildid=${env.BUILD_ID},commitid=${GIT_COMMIT}";
                    def uploadSpec = """{
                    "files": [
                    {
                    "pattern": "jarstaging/(*)",
                    "target": "ngk-libs-release-local/{1}",
                    "flat": "false",
                    "props": "${properties}",
                    "exclusions": ["*.sha1", "*.md5"]
                    }
                    ]
                    }"""
                    def buildInfo = server.upload(uploadSpec)
                    buildInfo.env.collect()
                    server.publishBuildInfo(buildInfo)
                }
            }
        }
        
    }
}

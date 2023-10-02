pipeline {
    agent{
        label 'JDK-17'
    }
    triggers{
        pollSCM('* * * * *')
    }
    stages{
        stage('vcs') {
           steps{
               git url: 'https://github.com/Bhavana-2022/pitstop.git',
                   branch: 'main'

        
            }
        }

        stage('build') {
            steps{
                sh(script: 'dotnet build src/pitstop.sln')


                rtUpload(
                    serverId: 'myinstance',
                    spec: """{
                        "files": [
                            {
                                "pattern": "**/*.dll",
                                "target": "pitstop-generic-local/pitstop-generic-local/"
                            }
                        ]
                    }""" 

                )

            }
        }

        stage('results') {
            steps{
                archiveArtifacts artifacts : '**/*.dll'
            }
        }    
    }    
        

}
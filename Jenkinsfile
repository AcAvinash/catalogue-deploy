pipeline {
    agent { node { label 'AGENT-1' } }
    stages {
        
        // here I need to configure downstram job. I have to pass package version for deployment
        // This job will wait until downstrem job is over
        stage('Deploy') {
            steps {
                script{
                    echo "Deployment"
                    def params = [
                        string(name: 'version', value: "$packageVersion")
                    ]
                    build job: "../catalogue-deploy", wait: true, parameters: params
                }
            }
        }
    }

    post{
        always{
            echo 'cleaning up workspace'
            //deleteDir()
        }
    }
}
pipeline {
    agent { node { label 'AGENT-1' } }
    parameters {
        string(name: 'version', defaultValue: '')
    }
    stages {
        
        // here I need to configure downstram job. I have to pass package version for deployment
        // This job will wait until downstrem job is over
        stage('Deploy') {
            steps {
                script{
                    echo "Deployment"
                    echo "Version received from upstream = ${params.version}"
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
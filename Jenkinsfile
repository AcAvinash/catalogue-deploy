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

        stage('Init'){
            steps{
                withAWS(credentials: 'aws', region: 'us-east-1') {
                    sh '''
                    cd terraform
                        terraform init

                    '''
                }
            }
        }

        stage('Plan'){
            steps{
                withAWS(credentials: 'aws', region: 'us-east-1') {
                    sh '''
                       cd terraform
                       terraform plan
                    '''
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
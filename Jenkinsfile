pipeline{
    agent any 
    stages{
        stage("Upload To A"){
            steps{
                withAWS(region:'eu-central-1',credentials:'aws-static'){
                    s3Upload(file:'index.html', bucket:'udacity-project-jenkins', pathStyleAccessEnabled: true, payloadSigningEnabled: true)
                }
            }
        }
    }
}
pipeline{
    agent any 
    stages{
        stage("Lint HTML"){
            steps{
                sh '''
                    echo "Linting HTML..."
                    tidy -q -e *.html
                '''
            }
        }
        stage("Upload To AWS"){
            steps{
                withAWS(region:'eu-central-1',credentials:'aws-static'){
                    s3Upload(file:'index.html', bucket:'udacity-project-jenkins', pathStyleAccessEnabled: true, payloadSigningEnabled: true)
                }
            }
        }
    }
}
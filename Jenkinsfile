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
        stage("Ensure content is up"){
            steps{
                sh '''
                        if curl --silent --head --fail "http://udacity-project-jenkins.s3-website.eu-central-1.amazonaws.com/" then \
                            echo "The content is up ... "; \
                            exit 0; \
                        else \
                            echo "This URL Not Exist !!"; \
                            exit 1; \
                        fi 

                '''
            }
        }
    }
}
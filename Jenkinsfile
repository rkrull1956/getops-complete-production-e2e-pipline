pipeline{
    agent{
        label "jenkins-agent"
    }
    environment{
        APP_NAME = 'complete-production-e2e-pipline'
    }

    stages{
        stage("Cleanup Workspace"){
            steps {
                cleanWs()
            }

        }
    
        stage("Checkout from SCM"){
            steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/rkrull1956/getops-complete-production-e2e-pipline'
            }

        }
        stage("Update the Deployment Tags"){
            steps {
                sh """
                    cat deploymnet.yaml
                    sed -i 's/${APP_NAME}.*/${APP_NAME):${IMAGE_TAG}/g' deployment.yaml
                    cat deployment.yaml
                """
            }

        }

        stage("Push the updated Deployment file to GIT"){
            stage {
                sh """
                    git config --global user.name "rkrull1956"
                    git config --global user.email "roger.krull@yahoo.com"
                    git add deployment.yaml
                    git commit -m "Updated Deployment Manifest"
                """
                withCredential((gitUserPassword(crendentialID:"gitbh-pat":gitTooName: 'Default'))) {
                    sh "get push ..... main"
                }
            }

        }



}

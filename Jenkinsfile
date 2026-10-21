pipeline{
    
    agent {lable "dev"};
    
    stages{
        stage("Code Clone"){
            steps{
                git url: "https://github.com/nishant-gupta7456/Two-tier.git", branch: "main"
            }
        }
        stage("Bulid"){
            steps{
                sh "docker build -t my-app:latest ."
            }
        }
        stage("Test"){
            steps{
                echo "Dev/tester test likh kr denge..."
            }
        }
        stage("Push to docker hub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId:"dockerHubCreds", 
                    passwordVariable:"dockerHubPass",
                    usernameVariable:"dockerHubUser"
                    )]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag my-app ${env.dockerHubUser}/my-app"
                sh "docker push ${env.dockerHubUser}/my-app:latest "
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker compose up -d --build flask-app"
            }
        }
    }
    
}

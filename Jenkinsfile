pipeline{
    agent any
    
    stages{
        stage(" Clone Code"){
            steps {
                echo "cloing the Code"
                git url: "https://github.com/thirupathi8790/django-note-app.git", branch: "main"
            }
        }
        stage("build"){
            steps {
                echo "build the image"
                sh "docker build -t my-node-app1 ."
            }
        }
        stage("Push to DockerHub"){
            steps {
                echo "push the image to the Docker HUb"
                withCredentials([usernamePassword(credentialsId: "DockerHub", passwordVariable: "DockerHubPass", usernameVariable: "DockerHubUser")]) {
                sh "docker tag my-node-app1 ${env.DockerHubUser}/my-node-app1:latest"    
                sh "docker login -u ${env.DockerHubUser} -p ${env.DockerHubPass}"
                sh "docker push ${env.DockerHubUser}/my-node-app1:latest"
  
                }
            }
        }
        stage("Deploy"){
            steps{
                echo "deply the container"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}

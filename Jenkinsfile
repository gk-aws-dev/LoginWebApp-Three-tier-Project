pipeline{
    agent{
        label{
            label "slave-ssh"
            customWorkspace "/opt/three-tier"  //you can mentioned custom working dir here
        }
    }
    tools {
        maven 'maven' // Use the name you configured in Jenkins for Maven
    }
    environment {
        url = "https://github.com/gk-aws-dev/project_java.git"
        url2 = "https://github.com/gk-aws-dev/docker-example.git"
       // devip = "172.31.33.102"
        
    }
    stages{
        stage ("clone repo"){
            steps{
                sh "rm -rf *"
                sh " git clone $url"
            }
        }
        stage ("buil-war"){
            steps{
                sh "cd project_java && mvn clean package -DskipTests=true"
            }
        }
        stage("docker-compose")
        {
        steps{
            //sh "rm -rf *"
            sh "git clone $url2"
            sh "cd docker-example && docker-compose down -v"
            sh "docker system prune -af"
            sh "cd docker-example && docker-compose up -d"
        }
        }
    }
}

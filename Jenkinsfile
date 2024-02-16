pipeline{
    agent any
    tools{
        nodejs "nodejs"
    }
    stages{
        stage("Clean Workspace"){
            steps{
                cleanWs()
            }
        }
        stage("Checkout From SCM"){
            steps{
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/jaatbreak/zomato.git'
            }
        }
        stage("Build Application"){
            steps{
                sh "npm install"
            }
        }
        stage("Test Application"){
            steps{
            sh  "npm install -g pm2"
            sh "pm2 start server.js"
                echo "Application is Test"
            }
        }
        stage("Sonarqube Analysis"){
            steps{
                withSonarQubeEnv(credentialsId:'sonarqube-token'){
                sh "sonarqube:sonar-scanner"
                }
            }
        }
        
    }
}

pipeline{
    agent any
    stages{
        stage("clone git code"){
            steps{
                git branch: 'master', credentialsId: 'git_credentials', url: 'https://github.com/kkarun-ges/sample-hello-world.git'
            }
        }
        stage("build code"){
            steps{
                sh "mvn clean package"
            }
        }
        stage("deploy code to tomcat server"){
            steps{
                sshagent(['deploy-tomcat-server']) {
                    sh 'scp -o StrictHostKeyChecking=no webapp/target/webapp.war ubuntu@ec2-35-167-55-80.us-west-2.compute.amazonaws.com:/opt/tomcat/apache-tomcat-8.5.68/webapps'
                }
            }
        }
    }
}

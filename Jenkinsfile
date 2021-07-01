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
        stage("deploy code to web-server using ansible"){
            steps{
                sshagent(['deploy-tomcat-server']) {
                    sh 'ansible-playbook ansible.yml -u ubuntu'
                }
            }
        }
    }
}

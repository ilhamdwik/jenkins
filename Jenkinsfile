def credential = 'ilhaskam'
def server = 'ubuntu@54.64.54.75'
def directory = '~/wayshub/wayshub-frontend'
def branch = 'master'
def images = 'ilhaskam/wayshub-frontend'
def username = 'awkawk'
def password = 'awkawk'

    
pipeline{
    agent any
    post{
      always{
             echo 'Your Build'
             discordSend description: '`Discord Notification is running`', footer: '', image: '', link: '', result: 'SUCCESS|UNSTABLE|FAILURE|ABORTED', scmWebUrl: '', thumbnail: '', title: 'Discord Notification', webhookURL: 'https://discord.com/api/webhooks/1055283274798342165/chuTPBsmyrmJABK7rPrWiBC7D9mzvg6876mcVbA9j_1yh-BjM8chLkqm8AjxD8HSIKUp'
         }
    }
    stages{
        stage ('git pull'){
            steps{
                sshagent([credential]) {
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${directory}
                    git pull origin ${branch}
                    exit
                    EOF"""
                }
            }
        }
        stage ('build docker image'){
            steps{
                sshagent([credential]) {
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${directory}
                    docker build -t ${images} .
                    exit
                    EOF"""
                }
            }
        }
        stage ('docker up'){
            steps{
                sshagent([credential]) {
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    cd ${directory}
                    docker-compose up -d
                    exit
                    EOF"""
                }
            }
        }
    }
}

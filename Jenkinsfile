pipeline {
    agent { 
        node {
            label 'docker-agent-python'
            }
      }
    triggers {
        pollSCM '*/5 * * * *'
    }
    stages {
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                cd myapp
                pip install -r requirements.txt
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                sh '''
                cd myapp
                python3 hello.py
                python3 hello.py --name=Sharon
                '''
            }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                echo "doing delivery stuff.."
                '''
                script {
                    def discordMessage = "¡Hola equipo! La entrega se realizó correctamente."
                    def discordWebhookUrl = 'https://discord.com/api/webhooks/1229594864224829520/CE19t6B6yKtN9veyZG2ew019l80tsel8XE-SGATrgHoyVsdNqvtaYNju0GBSBNa_aXRC'
                    httpRequest(
                        contentType: 'APPLICATION_JSON',
                        url: discordWebhookUrl,
                        requestBody: "{\"content\": \"${discordMessage}\"}"
                    )
                }
            }
        }
    }
}
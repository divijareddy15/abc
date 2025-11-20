 pipeline {
    agent any
    tools {
        maven 'Maven-3.9.11'
    }
    stages {
        stage('Clone Git Repo & Clean') {
            steps {
                bat 'if exist mavenjava rmdir /s /q mavenjava'
                bat 'git clone https://github.com/srivyshnavi18/maven-java-project.git mavenjava'
                bat 'mvn clean -f mavenjava/pom.xml'
            }
        }
        stage('Install') {
            steps {
                bat 'mvn install -f mavenjava/pom.xml'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test -f mavenjava/pom.xml'
            }
        }
        stage('Package') {
            steps {
                bat 'mvn package -f mavenjava/pom.xml'
            }
        }
    }
}



# ngrk 
1.ngrok config add-authtoken <your_token>
2.ngrok http 8080
3.Open your GitHub Repo → Settings → Webhooks
Click Add Webhook
Set:
Payload URL
https://abcd1234.ngrok.io/github-webhook/
Content type
application/json
4.Click Add webhook
5.✅ Step 4 — Configure Jenkins
Open Jenkins → Your Job → Configure
Enable:
✔ GitHub hook trigger for GITScm polling
Save.
🎉 RESULT:
Every push to GitHub → triggers Jenkins automatically through ngrok.

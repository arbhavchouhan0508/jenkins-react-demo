pipeline {
    agent any

    tools {
        nodejs 'node18'
    }
    environment {
        VERCEL_TOKEN = credentials('vercel-token')
    }

    stages {
        stage('Check Node') {
            steps {
                sh 'node -v'
                sh 'npm -v'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build App') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy to Vercel') {
            steps {
                sh '''
                  vercel pull --yes --environment=production --token=$VERCEL_TOKEN
                  vercel build --prod --token=$VERCEL_TOKEN
                  vercel deploy --prebuilt --prod --token=$VERCEL_TOKEN
                '''
            }
        }
    }
}
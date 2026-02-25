pipeline {
    agent any

    environment {
        VERCEL_TOKEN = credentials('vercel-token')
    }

    stages {

        stage('Check Environment') {
            steps {
                sh 'node -v'
                sh 'npm -v'
                sh 'vercel --version'
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
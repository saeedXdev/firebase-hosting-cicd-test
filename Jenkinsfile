pipeline {
    agent any

    environment {
        FIREBASE_SA_KEY = credentials('FIREBASE_SA_KEY')
    }

    stages {
        stage('scm') {
        steps {
            git branch: 'main', url: 'https://github.com/saeedXdev/firebase-hosting-cicd-test.git'
           }
        }
        stage('Npm Install') {
            steps {
                script {
                        sh 'node -v'                
                        sh 'npm i || true'
                        // sh 'npm install -g firebase-tools'
                }
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build || true'
            }
        }
        stage('Inject GCP Credentials') {
            steps {
                withCredentials([file(credentialsId: 'FIREBASE_SA_KEY', variable: 'FIREBASE_KEY')]) {
           sh '''
               node -v
               firebase --version
               export GOOGLE_APPLICATION_CREDENTIALS="$FIREBASE_KEY"
               firebase deploy --only hosting --project "flappy-bird-game-c8ec7"
           '''
         }

            }
        }
       
    
        // stage('Deploy to Firebase') {
        //     steps {
        //          script {
        //             nodejs(nodeJSInstallationName: 'nodejs18'){                       
        //                 sh 'firebase --help'
        //                 // sh 'npm install -g firebase-tools'
        //             }
        //         }
                
                
                // sh 'npx firebase deploy --only hosting --non-interactive'
    
    }

}

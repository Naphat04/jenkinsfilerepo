pipeline {

    agent  any


  environment {
    VERCEL_PROJECT_NAME = 'learn-jenkins-app'
    VERCEL_TOKEN = credentials('VERCEL_TOKEN_ID') // ดึงจาก Jenkins
  }



  stages {
    stage('Test npm') {
      steps {
          sh 'npm --version'
          sh 'node --version'
        }
    }
    stage('Build') {
      steps {
          sh 'npm ci'
      }
      
    }
    stage('Test Build') {
      steps {
          sh 'npm run test'
      }
    }

    stage('Deploy') {
      steps {

          sh 'npm install -g vercel@latest'
          // Deploy using token-only (non-interactive)
          sh '''
            vercel link --project $VERCEL_PROJECT_NAME --token $VERCEL_TOKEN --yes
            vercel --token $VERCEL_TOKEN --prod --confirm
          '''
      }
    }
 
  }
}
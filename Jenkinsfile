pipeline {
    agent any
    
    tools {
        nodejs 'node20' // ต้องชื่อเดียวกับที่ตั้งใน Jenkins Tools
    }

    environment {
        
        
        // ดึง "กุญแจ" จาก Jenkins Credentials (ชื่อ ID ต้องตรงกัน)
        VERCEL_PROJECT_NAME = 'jenkins-lab-quiz'
        VERCEL_TOKEN = credentials('VERCEL_TOKEN_ID')
    }

    stages {
        stage('Test npm') {
            steps {
                sh 'npm install'
                sh 'node -v'
                echo 'Stage 1: Test npm passed!'
            }
        }

        stage('Build') {
            steps {
                echo 'Stage 2: Build passed!'
            }
        }

        stage('Test Build') {
            steps {
                // เช็คว่ามีโฟลเดอร์ผลลัพธ์การ Build จริงไหม
                sh 'ls -al'
                sh 'ls -R | grep -E "dist|build|.next"'
                echo 'Stage 3: Test Build passed!'
            }
        }

        stage('Deploy') {
            steps {
                // สั่ง Deploy ไป Vercel
                sh "vercel link --project $VERCEL_PROJECT_NAME --token $VERCEL_TOKEN --yes"
                sh "npx vercel --token ${VERCEL_TOKEN} --prod --yes"
                echo 'Stage 4: Deploy passed!'
            }
        }
    }
}
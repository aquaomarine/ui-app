

pipeline{
    agent {
        docker { image 'node:14-alpine' }
    }
    environment{
        CI = true
        HOME = '.'
        npm_config_cache = 'npm-cache'
    }
    stages{
        stage('install packages'){
            steps{
                sh 'npm install'
            }
        }
         stage('Test'){
            steps{
                sh 'npm test'
            }
        }
    }
    post { 
        always { 
           mail bcc: '', body: 'Check console output at &QUOT;<a href=\'${env.BUILD_URL}\'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>', cc: '', from: '', replyTo: '', subject: 'STARTED: Job \'${env.JOB_NAME} [${env.BUILD_NUMBER}]\'', to: 'admin@mail.com'
        }
    }
}


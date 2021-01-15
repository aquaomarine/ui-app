

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
}
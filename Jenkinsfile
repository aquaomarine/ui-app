

pipeline{
    agent{
        docker{
            image 'node:alpine'
             args '-p 20001-20100:3000'
        }
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
    }
}
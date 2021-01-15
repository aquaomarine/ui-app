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
                // sh "script.sh/bat"
            }
        }
        stage('Test'){
            steps{
                sh 'npm test'
            }
        }
        stage('Build for production'){
            steps{
                sh 'npm run build'
            }
        }

        // stage('staging'){
        //     steps{
        //         //
        //         input "deploy to production?"
        //     }
        // }   

        stage('deployment'){
            steps{
                withAWS(credentials: 'aws_credentials', region: 'ap-south-1') {
                    // some block
                    s3Delete bucket: 'nagcloudlab-ui', path: '**/*'
                    s3Upload acl: 'PublicRead', bucket: 'nagcloudlab-ui',includePathPattern: '**/*', workingDir: 'build'
                    mail(subject: 'Production Build', body: 'New Deployment to Production', to: 'jenkins-mailing-list@mail.com')
                }
            }
        }   
    }    
}


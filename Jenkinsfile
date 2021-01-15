
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
        stage('Build for production'){
            steps{
                sh 'npm run build'
            }
        }

        stage('deployment'){
            steps{
                withAWS(credentials: 'aws_credentials', region: 'ap-south-1') {
                    // some block
                    s3Delete bucket: 'nagcloudlab-ui', path: '**/*'
                    s3Upload acl: 'PublicRead', bucket: 'nagcloudlab-ui', cacheControl: '', excludePathPattern: '', file: '', includePathPattern: '**/*', metadatas: [''], redirectLocation: '', sseAlgorithm: '', tags: '', text: '', workingDir: 'build'
                    mail(subject: 'Staging Build', body: 'New Deployment to production', to: 'nagcloudlab@gmail.com')
                }
            }
        }    


    }
    post { 
        always { 
            // mail body: "<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p><p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>", subject: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'", to: 'admin@mail.com'
        }
    }
}


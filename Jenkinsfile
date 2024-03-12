    pipeline {
        
        agent any 
        
        environment {
            IMAGE_TAG = "${BUILD_NUMBER}"
        }
        
        stages {
            
            stage('Checkout'){
            steps {
                    git credentialsId: '0c75a505-8ae5-48ec-ba32-e97e52a355d5', 
                    url: 'https://github.com/phaneendra-github/sample-nextjs',
                    branch: 'feature/1'
            }
            }

            stage('Build Docker'){
                steps{
                    script{
                        sh '''
                        echo 'Buid Docker Image'
                        pwd
                        docker build -t hh-ui-nodejs:${BUILD_NUMBER} .
                        '''
                    }
                }
            }

            stage('Push the image'){
            steps{
                    script{
                        
                            sh '''                                                                    
                            aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 628976729859.dkr.ecr.us-east-1.amazonaws.com
                            docker tag hh-ui-nodejs:${BUILD_NUMBER} 628976729859.dkr.ecr.us-east-1.amazonaws.com/sampleecsjenkins:v${BUILD_NUMBER}
                            docker push 628976729859.dkr.ecr.us-east-1.amazonaws.com/sampleecsjenkins:v${BUILD_NUMBER}
                            '''
                        
                    }
                }
            }     
                
        }
    }

pipeline {
    agent any
      environment {
        BitBucket_Repo = ''
        Repo_Branch    = 'master'
    }
    stages {
    
        
        // Clone BitBucket Repo
        stage('Clone BitBucket Repo') {
        steps{  
           git branch: 'master', credentialsId: '8c91a177-f7ec-438f-9249-4ee20f8c4d62', url: 'https://ijehangirkhan@bitbucket.org/ijehangirkhan/testrepo.git'
            }
        }
        
        // Upload Chef Cookbooks
        stage('Upload Chef Cookbooks') {
        steps{
            sh '''cd chef-repo
            knife upload cookbooks -c /home/ubuntu/.chef/config.rb --chef-repo-path .
            cd ..
            echo "The cookbook uploaded successfully at $(date -u)" >> cookbookchange.txt
            cd ..'''
            }
        }
        
    }
    
        post { 
            always { 
                sh 'BITBUCKET_REPO_NAME=$(echo $GIT_URL | cut -d\'/\' -f 5 | cut -d\'.\' -f 1);'
                sh 'cd ..'
                sh 'rm -rf ${BITBUCKET_REPO_NAME}'
                sh 'rm -rf chef-repo'
                sh 'rm -rf cookbookchange.txt'
                sh 'rm -rf README.md'
                }
        }

}

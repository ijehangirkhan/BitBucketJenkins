pipeline {
    agent any
    stages {
        
        // Copy Chef Repository
        stage('Copy Chef Repository') {
        steps{  
           sh 'BITBUCKET_REPO_NAME=$(echo $GIT_URL | cut -d\'/\' -f 5 | cut -d\'.\' -f 1);'
           sh 'cd ..'
           sh 'cp -r /home/ubuntu/chef-repo ~/workspace/${JOB_BASE_NAME}/${BITBUCKET_REPO_NAME}'
            }
        }
        
        // Upload Chef Cookbooks
        stage('Upload Chef Cookbooks') {
        steps{  
            sh '''cd ~/workspace/${JOB_BASE_NAME}/${BITBUCKET_REPO_NAME}
            cd chef-repo
            knife upload cookbooks
            cd ..
            echo "The cookbook uploaded successfully at $(date -u)" >> cookbookchange.txt
            cd ..'''
            }
        }
    }
      
       post { 
        always { 
            sh 'cd ..'
            sh 'rm -rf ${BITBUCKET_REPO_NAME}'
            sh 'rm -rf chef-repo'
            sh 'rm -rf changes.txt'
            sh 'rm -rf cookbookchange.txt'
            sh 'rm -rf README.md'
            }
        }


}

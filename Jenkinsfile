pipeline{
    agent {
        docker{
            image 'ruby'
        }
    }

    stages{
        stage('Build'){
            steps {
                echo 'Building or resolve dependencies!'
                sh 'bundle install'
            }
        }
        
        stage('Tests'){
            steps {
                echo 'Running regression tests!'
            }
        }
        
        stage('UAT'){
            steps {
                echo 'Wait for user acceptance!'
                input(message:'Go to production?', ok: 'Yes')
            }
        }
        
        stage('PROD'){
            steps {
                echo 'WebApp is ready!'
            }
        }
            
    }
}
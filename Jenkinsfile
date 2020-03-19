pipeline{
    agent {
        docker{
            image 'qaninja/rubywd'
        }
    }

    stages{
        stage('Build'){
            steps {
                echo 'Building or resolve dependencies!'
                sh 'rm -f Gemfile.lock'
                sh 'bundle install'
            }
        }
        
        stage('Tests'){
            steps {
                echo 'Running regression tests!'
                sh 'bundle exec cucumber -p ci'
            }
        }
        post {
            always {
                cucumber failedFeaturesNumber: -1, failedScenariosNumber: -1, failedStepsNumber: -1, fileIncludePattern: '**/*.json', jsonReportDirectory: 'logs', pendingStepsNumber: -1, skippedStepsNumber: -1, sortingMethod: 'ALPHABETICAL', undefinedStepsNumber: -1
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
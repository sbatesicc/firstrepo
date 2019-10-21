pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo "We Building"'
                sh '''
                    echo "Multiline shell steps works too in Build stage"
                    ls -lah
                '''
            }
        }
		stage('Test') {
            steps {
                sh 'echo "We Testing"'
                sh '''
                    echo "Multiline shell steps works too in Test stage"
                    ls -lah
                '''
            }
        }
		stage('Deploy') {
            steps {
                sh 'echo "We Deploying now"'
                sh '''
                    echo "Multiline shell steps works too in Deploy stage"
                    ls -lah
                '''
				retry(3) {
                    sh './flakey-deploy.sh'
                }

                timeout(time: 3, unit: 'MINUTES') {
                    sh './health-check.sh'
                }
            }
        }
    }
	post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}

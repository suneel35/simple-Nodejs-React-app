pipeline {

  agent { label 'master' }

  options {

    disableConcurrentBuilds()
    timeout(time: 10, unit: 'MINUTES')
    buildDiscarder(logRotator(numToKeepStr: '10'))

  } 

environment {
            CI = 'true'
        }
    stages {
        stage('Build') {
            steps {
		sh 'scp -r /var/lib/jenkins/workspace/simple/ ubuntu@52.70.63.59:/opt/deployment'
                sh 'npm install'
            }
        } //Build
        stage('Test') {
                    steps {
			sh 'scp -r /var/lib/jenkins/workspace/simple/ ubuntu@52.70.63.59:/opt/deployment'
                        sh './jenkins/scripts/test.sh'
                    }
                } //Test
                stage('Deliver') {
                            steps {
				sh 'scp -r /var/lib/jenkins/workspace/simple/ ubuntu@52.70.63.59:/opt/deployment'
                                sh './jenkins/scripts/deliver.sh'
                                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                                sh './jenkins/scripts/kill.sh'
                            }
                        } // Deliver
 





} // pipeline

pipeline {
	agent any
	stages {
		stage('git checkout'){
			steps {
				checkout scm
			}
		}
		stage('docker build and push'){
			steps {
				sh 'cd test-nodeapp-1-task-2 && docker build . -t 097514400117.dkr.ecr.us-east-1.amazonaws.com/ravimmrepo:v${BUILD_NUMBER}'
				sh 'docker push 097514400117.dkr.ecr.us-east-1.amazonaws.com/ravimmrepo:v${BUILD_NUMBER}'
				sh 'docker rmi 097514400117.dkr.ecr.us-east-1.amazonaws.com/ravimmrepo:v${BUILD_NUMBER}'
			}
		}
		stage('docker deploy') {
			steps {
				sh 'cd /home/ubuntu/ansible && ssh -o StrictHostKeyChecking=no -i jenkins.pem ubuntu@10.0.2.54'
				sh 'docker pull 097514400117.dkr.ecr.us-east-1.amazonaws.com/ravimmrepo:v${BUILD_NUMBER} && docker run -itd -p 5000:8081 097514400117.dkr.ecr.us-east-1.amazonaws.com/ravimmrepo:v${BUILD_NUMBER}'
			}
		}
	}
}
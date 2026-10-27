# JenkinsFile for our CI CD Server
pipeline {
	agent any

	stages {

		stage('Build Backend') {
			steps {
				sh 'docker build -t nholmesdev/skillcheck-backend:latest codebase/backend
			}
		}

		stage('Build Frontend') {
			steps {
				sh 'docker build -t nholmesdev/skillcheck-frontend:latest codebase/frontend'
			}
		}

		stage('Push Images') {
			steps {
				withCredentials([usernamePassword(
					credentialsId: 'dockerhub-creds',
					usernameVariable: 'DOCKER USER',
					passwordVariable: 'DOCKER_TOKEN'
				)]) {
				sh 'echo "$DOCKER_TOKEN" | docker login -u "$DOCKER_USER" --password-stdin'
				sh 'docker push nholmesdev/skillcheck-backend:latest'
				sh 'docker push nholmesdev/skillcheck-frontend:latest'
				}
			}
		}

		stage('Deploy') {
			steps {
				sh 'kubectl apply -f kubernetes/ -n skillcheck'
				sh 'kubectl rollout restart deployment/backend deployment/frontend -n skillcheck'
				sh 'kubectl rollout status deployment/backend -n skillcheck'
				sh 'kubestl rollout status deployment/frontend -n skillchecl'
			}
		}
	}
}

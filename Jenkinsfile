node {
  try  {
	def app
		stage('Clone Repository') {
			checkout scm
		}

	stage('Build Image') {
		app = docker.build("shroderdog/exampleapp")
	}

	stage('Test JS') {
		app.inside {
			sh 'npm test'
		}
	}

	stage('Push image') {
		docker.withRegistry('', 'clay_docker_hub') {
			app.push("latest")
		}
	}
    } catch(error) {
                withCredentials([[$class: 'StringBinding', credentialsId: '	slack-jenkins', variable: 'SLACK_URL']]) {
                    sh "curl -XPOST -d 'payload={ \"color\": \"danger\", \"text\": \":warning: Build failed: $error (see <${env.BUILD_URL}/console|the build logs>)\" }' ${env.SLACK_URL}"
                    }
        }
}


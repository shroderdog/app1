node {

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
}

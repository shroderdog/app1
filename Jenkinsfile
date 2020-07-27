node {

      def app
      stage 'Clone Repository' {
          checkout scm
      }

      stage ('Build Image') {
           app = docker.build("shroderdog/exampleapp")
      }

      stage('Push image') {
           docker.withRegistry('https://registry.hub.docker.com', 'clay_docker_hub') {
               app.push("latest")
           }
      }
}

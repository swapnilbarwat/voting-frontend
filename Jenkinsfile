def version = ''
node {
   stage('checkout') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/swapnilbarwat/voting-frontend.git'
      version = readFile('version').trim()
      currentBuild.displayName = "${version}-${env.BRANCH_NAME}"
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
   }
   stage('Build') {
       docker.withRegistry('https://docker.io', 'docker-hub-credentials') {
          def app = docker.build("harshals/voting-frontend:${version}")
          sh "docker push docker.io/harshals/voting-frontend:${version}"
       }
       sh "curl -H \"Content-Type: application/x-yaml\" -X POST http://104.154.240.64:8080/api/v1/breeds --data-binary @deployment/breeds/redis.yml"
       sh "curl -H \"Content-Type: application/x-yaml\" -X POST http://104.154.240.64:8080/api/v1/breeds --data-binary @deployment/breeds/voting.yml"
    }
}

node {
   stage('50-50% deployment') { // for display purposes
      input message: 'Deploy to cluster? This will rollout new build to 50% cluster.'
      
      sh "curl -H \"Content-Type: application/x-yaml\" -X PUT http://104.154.240.64:8080/api/v1/deployments/voting_frontend --data-binary @deployment/blueprint.yml"
      sh "curl -H \"Content-Type: application/x-yaml\" -X PUT http://104.154.240.64:8080/api/v1/gateways --data-binary @deployment/gateway.yml"
   }
}

node {
   stage('move full') { // for display purposes
      input message: 'Deploy to full cluster?'
   }
   stage('undeploy previous version') {
      echo "undeploying cluster"
   }
}
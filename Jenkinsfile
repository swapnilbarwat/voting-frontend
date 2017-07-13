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
       docker.withRegistry('http://104.154.183.130:5000') {
          def app = docker.build "voting-frontend:${version}"
          app.push("${version}")
       }
    }
}
stage "Deploy to dev. Mouse hover to select the option."
input message: 'Do you want to deploy?', submitter: 'Yes'
node {
   stage('deployment to dev') { // for display purposes
     echo "This will checkout blueprint yaml and deploy"
   }
}
stage "Deploy to production. Mouse hover to select the option."
input message: 'Do you want to deploy?', submitter: 'Yes'
node {
   stage('deployment to production') { // for display purposes
     echo "This will checkout blueprint yaml and deploy to production"
   }
}
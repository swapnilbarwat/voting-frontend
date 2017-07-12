node {
   def mvnHome
   stage('checkout') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/swapnilbarwat/voting-frontend.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
   }
   stage('Build') {
       docker.withRegistry('104.154.183.130:5000') {
          def app = docker.build "voting-frontend"
          version=$(cat version)
          app.push $version
       }
}
stage "Deploy to dev. Mouse hover to select the option."
input message: 'Do you want to deploy?', submitter: 'Yes'
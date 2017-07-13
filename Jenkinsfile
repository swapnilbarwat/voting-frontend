node {
   def mvnHome
   def version
   stage('checkout') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/swapnilbarwat/voting-frontend.git'
      version = readFile('version').trim()
      currentBuild.displayName = ${version}
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
   }
   stage('Build') {
       docker.withRegistry('http://104.154.183.130:5000') {
          def app = docker.build "voting-frontend:${version}"
          app.push(${version}")
       }
    }
}
stage "Deploy to dev. Mouse hover to select the option."
input message: 'Do you want to deploy?', submitter: 'Yes'
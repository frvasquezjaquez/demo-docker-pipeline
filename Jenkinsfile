node {
    label 'Azure-InsightVM'
   // Define a variable to use across stages
   def my_image
   stage('Build') {
       // Get Dockerfile and code from Git (or other source control)
       checkout scm
       // Build Docker image and set image reference
       my_image = docker.build("insightvm.pitafoo.com:5000/demo:${env.BUILD_ID}")
       echo "Built image ${my_image.id}"
   }
   stage('Test') {
       // Assess the image
        // assessContainerImage failOnPluginError: true,
        //   imageId: "${my_image.id}",
        //   thresholdRules: [
        //       exploitableVulnerabilities(action: 'Mark Unstable', threshold: '1')
        //     ],
        //     nameRules: [
        //       vulnerablePackageName(action: 'Fail', contains: 'nginx')
        //   ]
        
        assessContainerImage failOnPluginError: true,imageId: "insightvm.pitafoo.com:5000/demo:${env.BUILD_ID}"
           
   }
   stage('Deploy') {
       echo "Deploying image ${my_image.id} to somewhere..."
       // Push image and deploy a container
       // This step should not normally be used in your script. Consult the inline help for details.
        withDockerRegistry(credentialsId: '5637788b-0c37-43bc-9597-c3fe97840208', url: 'https://insightvm.pitafoo.com:5000') {
            my_image.push()
        
            
        }
   }
}
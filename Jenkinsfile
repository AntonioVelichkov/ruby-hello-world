@Library('mpl@av-test') _
AwsContainerPipeline {
  agent_label = 'central'
  appName = 'av-test-app'
  region = 'eu-west-1'
  terraformBranch = 'master'
  progLanguage = 'javascript'

  // Regression test in new test account
  businessUnit = 'devops-demo'
  awsAccountID = '349770967735'  
  environmentType = 'test'
  ecrRegistry = '836934336700.dkr.ecr.eu-west-1.amazonaws.com'
  modules.Deploy.lbName = 'demodynamo' 
  
  // Deploy to EKS
  modules.Checkout.failBuildOnDiscovery = false
  buildType = 'Maven'
  modules.Build.command = 'chmod +x mvnw && ./mvnw package'
  modules.Build.dockerBuildMemory = '512m'
  
  target = 'EKS'
  modules.Deploy.loadbalancerPort = '80'
  modules.Deploy.loadbalancerHttpsPort = '443'
  modules.Deploy.targetPort = '8080'
  modules.Deploy.appPort = '8080'
  modules.Deploy.replicas = '2'
  modules.Deploy.eksClusterName = 'sandbox-cluster'
  modules.Deploy.containerCpuLimit = '1.0'
  modules.Deploy.containerMemoryLimit = '1048M'
  modules.Deploy.containerCpuRequest = '400m'
  modules.Deploy.containerMemoryRequest = '256M'
  
  //skipTest            = true    // to skip gauntlt scans, jobs are getting aborted due to unreachable DNS endpoint comment once fixed
  modules.Test.nmapField = '80.tcp.*'
  //modules.Test.nmapField = "80/tcp\\s+open\\s+http"                      //What ports we expect to be open at application endpoint
  modules.Test.failBuildOnFailure = 'false'                              //fail buld on error or let is pass
  modules.Test.gauntltTags = '@normal'                                   //specify more tags e.g. @normal,@smoke
  modules.Test.gauntltReportFormat = 'html'                              //2 options, html or json
  modules.Test.applicationProtocol = 'http'  

  // ECR Scanning
  checkECRImage = true                 //use ECR native image scanning capability
  imageHighVulnCount = '3'               //number of high vulnerability issues allowed 
  imageMediumVulnCount = '10'            //number of medium vulnerability issues allowed 
  imageLowVulnCount = '20'               //number of low vulnerability issues allowed

  enableSelenium = false
  enableSonarQube = false
  //sonarProjectName = 'elmpetclinic-eks'
  //sonarProjectKey = 'SPC-elmpetclinic-eks'
    
  skipArtifactory = true
  enableDebug = true
  destroyApp = true

  //skipBuild = true
}
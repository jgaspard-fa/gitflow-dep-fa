
properties([[$class: 'ParametersDefinitionProperty', parameterDefinitions: [[$class: 'StringParameterDefinition', defaultValue: 'top10dependency', description: 'Some Description', name : 'repository'], [$class: 'StringParameterDefinition', defaultValue: 'source-javadoc,unit', description: 'Some Description', name: 'profile']]]])

node {
    
   // Mark the code checkout 'stage'....
   stage 'Checkout'
   
   print "DEBUG: parameter repository = ${repository}"

   // Get some code from a GitHub repository
   //non git url: 'git@github.com:financeactive/' + repository + '.git'
   //ok git url: 'https://github.com/jgaspard-fa/' + repo + '.git'
   //non git url: 'https://github.com/financeactive/' + repository
   git branch: 'develop', credentialsId: 'jgaspard-fa-https', url: 'https://github.com/financeactive/top10'

   // Get the maven tool.
   // ** NOTE: This 'M3' maven tool must be configured
   // **       in the global configuration.           
   def mvnHome = tool 'M3'

   // Mark the code build 'stage'....
   stage 'Build'
   // Run the maven build
   sh "${mvnHome}/bin/mvn -Dmaven.test.skip=true -P${profile} clean package"
   step([$class: 'JUnitResultArchiver', testResults: '**/target/surefire-reports/TEST-*.xml'])
}
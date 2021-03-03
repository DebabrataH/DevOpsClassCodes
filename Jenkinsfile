
pipeline{
    tools{
        jdk 'myjava'
        maven 'mymvn'
    }
    agent none
      stages{
           stage('Checkout'){
               agent Linux_mumbai_AG
               steps{
                 git 'https://github.com/DebabrataH/DevOpsClassCodes.git'
              }
          }
          stage('Compile'){
              agent any
              steps{
                  echo 'compiling'
                  sh 'mvn compile'
              }
          }
          stage('CodeReview'){
              agent any
              steps{
                  sh 'mvn pmd:pmd'
              }
          }
           stage('UnitTest'){
               agent any
              steps{
                  sh 'mvn test'
              }
               post {
               success {
                   junit 'target/surefire-reports/*.xml'
               }
           }	
          }
           stage('MetricCheck'){
               agent Linux_mumbai_AG
              steps{
                  sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
              }
               post {
               success {
	           cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false                  
               }
           }		
          }
	  stage('make a directory and file'){
	       agent Linux_mumbai_AG
		  steps{
		      echo ('Hello World')  
		      sh ('rmdir File2')
		      sh ('rm file2.txt')
	       }
	  }
	  stage('Package'){
              agent any
              steps{
                  sh 'mvn package'
              }
          }
          
      }
}

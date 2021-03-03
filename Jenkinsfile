
pipeline{
    tools{
        jdk 'myjava'
        maven 'mymvn'
    }
    agent master
      stages{
           stage('Checkout'){
               agent master
               steps{
                 git 'https://github.com/DebabrataH/DevOpsClassCodes.git'
              }
          }
          stage('Compile'){
              agent master
              steps{
                  echo 'compiling'
                  sh 'mvn compile'
              }
          }
          stage('CodeReview'){
              agent master
              steps{
                  sh 'mvn pmd:pmd'
              }
          }
           stage('UnitTest'){
               agent master
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
               agent master
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
	       agent Slave_MumbaiLinux
		  steps{
		      echo ('Hello Wor')  
		      sh ('mkdir Fil')
		      sh ('touch file3.txt')
	       }
	  }
	  stage('Package'){
              agent master
              steps{
                  sh 'mvn package'
              }
          }
          
      }
}

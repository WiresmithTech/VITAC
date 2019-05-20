node {
  try {
  
	stages {
	
		stage ('Checkout') {
			checkout scm
		}


		stage ('Unit Test') {
			   bat "labview-cli -v --lv-ver 2015 \"C:\\Users\\Public\\Documents\\National Instruments\\LV-CLI Common Steps\\steps\\run-vi-tester.vi\" -- \"VITAC.lvproj\" \"test_results.xml\" \"${env.WORKSPACE}\""
			   junit "test_results.xml"
		}

		stage ('Build Output') {
			bat "\"C:\\Program Files (x86)\\National Instruments\\LabVIEW 2011\\LabVIEW.exe\" \"C:\\Users\\Public\\Documents\\National Instruments\\LV-CLI Common Steps\\steps\\vipbBuild.vi\" -- \"VITAC (VI Tester Advanced Comparisons).vipb\" Builds  \"${env.WORKSPACE}\""

		}
	}
	
	post {
	always {
		dir ("Builds") {
			archiveArtifacts artifacts: '*.vip', fingerprint: true
			deleteDir()
		}

	}
}
   } catch(any) {
    currentBuild.result = 'FAILURE'
    throw any //rethrow exception to prevent the build from proceeding
   } finally {
            step([$class: 'Mailer', notifyEveryUnstableBuild: true, recipients: 'james@wiresmithtech.com', sendToIndividuals: true])
   }
}
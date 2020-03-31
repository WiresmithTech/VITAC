pipeline {
  agent {
    node {
      label 'LV2015'
    }
  }
  environment {
    LV_VER = 2015
	LV_BIT = 32
    G_CLI_PARAMS = "--lv-ver ${env.LV_VER}"
	VERSION = "1.3.1"
	FULL_VERSION = VersionNumber(versionNumberString: '${BUILDS_ALL_TIME,X}', versionPrefix: "${VERSION}." , worstResultForIncrement: 'FAILURE') 
  }
  options {
    timeout(time:45, unit: 'MINUTES')
	buildDiscarder(logRotator(numToKeepStr: '100'))
  }
  stages {
    stage('Setup') {
      steps {
	    script {
		  currentBuild.displayName = "${env.FULL_VERSION}"
		}
		echo "Building ${FULL_VERSION}"
		bat "if not exist builds mkdir builds"
      }
    }
	

    stage('Unit Test') {
      steps {
        bat 'g-cli %G_CLI_PARAMS% viTester --  -xml "test_results.xml" "VITAC.lvproj"'
		junit 'test_results.xml'
      }
    }
    stage('Build Outputs') {
      steps {
		bat 'g-cli %G_CLI_PARAMS% vipBuild -- -versionNumber %FULL_VERSION% "VITAC (VI Tester Advanced Comparisons).vipb"'
		dir ("builds") {
			archiveArtifacts artifacts: '*.vip', fingerprint: true
			deleteDir()
		}

      }
    }

	stage('Release Steps') {
		when { buildingTag() }
		steps {
		    script {
			  currentBuild.description = "${env.VERSION} Release"
			  currentBuild.keepLog = true
			}
		}
	}
  }
  post {
    always {
      step([$class: 'Mailer', notifyEveryUnstableBuild: true, recipients: emailextrecipients([culprits(), requestor(), upstreamDevelopers()]), sendToIndividuals: true])
	  bat 'g-cli %G_CLI_PARAMS% quitLabVIEW'
    }

  }
  
}
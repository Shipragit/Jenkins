pipeline {
    agent any
    environment {
        BRANCH = "${BRANCH_NAME}"
        APPSYSID = 'f70d8b8d1bf706100efe5242604bcb47'
        CREDENTIALS = '2eccede0-b38e-40f7-9733-1aba40f671e8'
        DEVENV = 'https://brightspeedtsmqa1.service-now.com/'
        TESTENV = 'https://testinstance.service-now.com/'
        PRODENV = 'https://prodinstance.service-now.com/'
        TESTSUITEID = 'b1ae55eedb541410874fccd8139619fb'
    }
    stages {
        stage('Build') {
            steps {
                snApplyChanges(appSysId: "${APPSYSID}", branchName: "${BRANCH}", url: "${DEVENV}", credentialsId: "${CREDENTIALS}")
                snPublishApp(credentialsId: "${CREDENTIALS}", url: "${DEVENV}", appSysId: "${APPSYSID}",
                        isAppCustomization: true, obtainVersionAutomatically: true, incrementBy: 2)
            }
        }
        /*stage('Install') {
            steps {
                snInstallApp(credentialsId: "${CREDENTIALS}", url: "${TESTENV}", appSysId: "${APPSYSID}", baseAppAutoUpgrade: false)
                snRunTestSuite(credentialsId: "${CREDENTIALS}", url: "${TESTENV}", testSuiteSysId: "${TESTSUITEID}", withResults: true)
            }
        }
        stage('Deploy to Prod') {
            when {
                branch 'master'
            }
            steps {
                snInstallApp(credentialsId: "${CREDENTIALS}", url: "${PRODENV}", appSysId: "${APPSYSID}", baseAppAutoUpgrade: false)
            }
        }*/
	   	 post {
    			failure {
        			mail to: 'shiva291291@gamil.com',
             				subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
             				body: "Something is wrong with ${env.BUILD_URL}"
    				}
			}
    }
}

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
                always {
                        emailext (
                                subject: "Pipeline status ${currentBuild.result}"
                                body: '''<html> 
                                                <body>
                                                        <P>Build Status: ${currentBuild.result}<P>
                                                        <P>Build Number: ${currentBuild.number}<P>
                                                        <P>Check the <a href="${evn.BUILD_URL}">console output</a>.</p>
                                                <body>
                                        <html>'''
                                to:'shiva291291@gmail.com',
                                from:'shiva291291@gmail.com',
                                replyTo:'shiva291291@gamil.com',
                                mimeType:'text/html'
                        )
                }
        }

    }
}

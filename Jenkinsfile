pipeline {
    environment {
imagename = "nagp_devops_3149268"
dockerImage = ''
}
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
    }

    stages {
        stage('Clone sources') {
            steps {
                // Get some code from a GitHub repository
                checkout scm
				}                
            }
			
		stage('build && SonarQube analysis') {
			tools{
			    jdk "JDK 11"
		    }
            steps {
		    script {
            scannerHome = tool 'SQ';
            bat "npm install"
        }
		            
                withSonarQubeEnv(credentialsId: '96785c03-6f43-4550-988b-c731513ff460', installationName: 'SQI') {
                    // Optionally use a Maven environment you've configured already
                    bat """
                        ${scannerHome}/bin/sonar-scanner \
                        -D sonar.projectKey=angular-starter \
                        -D sonar.projectName=angular-starter \
                        -D sonar.projectVersion=1.0 \
                        -D sonar.sources=./src \
                        -D sonar.exclusions=**/node_modules/**
                        """
                }
            }
        }
        /*stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
                    waitForQualityGate abortPipeline: true
                }
            }
        }*/
	    
		
		/*stage("Build and run tests"){
			steps{
				bat "mvn -Dmaven.test.failure.ignore=true clean package"
			}
			post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the war file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    //archiveArtifacts 'test-output/*'
                }
            }
		}*/
	    
	    
		
		/*stage("Build docker image"){
			steps{
			script{
				dockerImage = docker.build imagename
			}
				
			}
		}
		stage("Run Image Container"){
			steps{
			script{
				dockerImage.run()
			}
				
			}
		}*/
	    /*stage('Publish report'){
		    steps{
			    script{
				publishHTML (target : [allowMissing: false,
 alwaysLinkToLastBuild: true,
 keepAll: true,
 reportDir: 'test-output',
 reportFiles: 'extentReport.html',
 reportName: 'My Reports',
 reportTitles: 'The Report'])    
			    }
		    }
	    }
	    stage('Email') {
    steps {
        script {
            def mailRecipients = "${params.recipients}"
            def jobName = currentBuild.fullDisplayName
	    zip zipFile: 'test.zip', archive: false, dir: 'test-output/Suite', overwrite: true
	    archiveArtifacts artifacts: 'test.zip', onlyIfSuccessful: true
            emailext body: '''${JELLY_SCRIPT, template="html-with-health-and-console"}''',
            mimeType: 'text/html',
            subject: "[Jenkins] ${jobName}",
            to: "${mailRecipients}",
            replyTo: "${mailRecipients}",		    
	    attachmentsPattern: 'test.zip, test-output/extentReport.html',
            recipientProviders: [[$class: 'CulpritsRecipientProvider']]
        }
    }
}*/	    
      }	
	post { 
        always { 
            echo 'I will always say Hello again!'
        }
		success {
      			build job: 'Automation Suite'
    		}
    	}
    }


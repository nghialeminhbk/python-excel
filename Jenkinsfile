pipeline {
	agent any

	stages {
		stage("Deploy") {
			steps {
				script {
                    def cmd = sh(script: "python3 app.py", returnStdout: true).trim()
                    sh "echo ${cmd}"
					cmd.each{e -> stage("Deploy to ${e}"){
						withAWS(region: "us-east-1"){
							sh """
							aws s3 ls
							"""
						}
					}}
				}
			}
		}
	}
}

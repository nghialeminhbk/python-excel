pipeline {
	agent any

	stages {
		stage("Dynamic Deployment") {
			steps {
				script {
					def environment = ["dev", "prd", "stg"]
					environment.each{e -> stage("Deploy to ${e}"){
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

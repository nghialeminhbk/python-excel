pipeline {
	agent any

	stages {
        stage("Prepare environment") {
            steps {
                sh """
                python3 -m venv venv
                source venv/bin/activate
                pip3 install -r requirements.txt
                """
            }
        }
		stage("Process check Account") {
			steps {
				script {
                    def cmd = sh(script: "python3 app.py", returnStdout: true).trim()
                    sh "echo ${cmd}"
                    def inputArr = cmd.replaceAll("\\[|\\]", "").split(",").collect { it as Integer }
					inputArr.eachWithIndex{e, index -> stage("Check Account: ${e}"){
						withAWS(region: "us-east-1"){
                            // sh "aws s3 ls --output text"
							rs = sh(script: "aws s3 ls --output text", returnStdout: true).trim()
                            if(rs.contains("nghiatitan")){
                                sh "python3 app.py ${index + 2}"
                            }
						}
					}}
				}
			}
		}
        stage("Push check file to s3") {

        }
	}
}

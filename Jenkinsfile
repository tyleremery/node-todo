node {
    def app
	def db

    stage('Clone repository') {
        checkout scm
    }

    stage('Build images') {
        app = docker.build("hw-app", ".")
		db = docker.build("hw-db", "./db")
    }

    stage('Push images') {
        docker.withRegistry('https://535625691106.dkr.ecr.us-east-1.amazonaws.com/', 'ecr:us-east-1:push-credential') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
			db.push("${env.BUILD_NUMBER}")
            db.push("latest")
        }
    }
}
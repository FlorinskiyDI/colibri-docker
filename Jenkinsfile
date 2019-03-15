node('docker') {

	stage 'Checkout'
		checkout scm

	stage 'Build & UnitTest'
		sh "docker build -t colibri.identity.api:B${BUILD_NUMBER} -f src/Services/Identity/Identity.API/Dockerfile ."

}
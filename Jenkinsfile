node('docker') {

	stage 'Checkout'
		checkout scm

	stage 'Build'
		sh "docker build -t colibri.identity.api:B${BUILD_NUMBER} -f src/Services/Identity/Identity.API/Dockerfile ."
		
	stage 'UnitTest'
		sh "docker build -t colibri.identity.api:test-B${BUILD_NUMBER} -f src/Services/Identity/Identity.API/Dockerfile.Integration ."
}
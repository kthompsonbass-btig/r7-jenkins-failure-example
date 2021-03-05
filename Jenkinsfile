pipeline {
    agent any
    environment {
        DOCKER_TAG = "test-r7-scanner:latest"
    }
    stages {
        stage('Docker') {
            steps {
                sh 'docker build --tag ${DOCKER_TAG} .'
            }
        }    
        stage('Rapid7 Scan') {
            steps {
                assessContainerImage failOnPluginError: true,
                    imageId: "${DOCKER_TAG}",
                    thresholdRules: [
                        criticalVulnerabilities(action: 'Fail', threshold: '1')
                    ]
            }
        }
    }
}

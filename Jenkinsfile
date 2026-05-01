pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building in the war'
            }
        }
        stage('Deploy to QA') {
            steps {
                echo 'Deploying to QA..'
            }
        }
       stage('Checkout') {
            steps {
                git 'https://github.com/BilalPeerjade/APIPostmanCollection'
            }
        }
        stage('pull Docker Image') {
            steps {
                bat 'docker pull peerjadebilal/gorestapitest:1.1'
            }
        }
	stage('Run API Test Cases') {
            steps {
                bat 'docker run -v %cd%/newman:/app/newman peerjadebilal/gorestapitest:1.1'
            }
        }
	stage('Publish HTML Extra Report') {
    	steps {
        publishHTML([
            allowMissing: false,
            alwaysLinkToLastBuild: false,
            keepAll: true,
            reportDir: 'newman',
            reportFiles: 'naveen.html',
            reportName: 'HTML Extra API Report',
            reportTitles: ''
        ])
    }
}
	stage("Deploy to PROD") {
    steps {
        echo "Deploying to PROD"
    }
}
	
    }
}
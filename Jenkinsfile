node {
    def nodeHome = tool name: 'node-6.11.2', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
    sh "${nodeHome}/bin/node -v"

    stage('check tools') {
        sh "node -v"
        sh "npm -v"
    }

    stage('checkout') {
        checkout scm
    }

    stage('npm install') {
        sh "npm install"
    }

    stage('unit tests') {
        sh "ng test --watch false"
    }

    stage('protractor tests') {
        sh "npm run e2e"
    }
}

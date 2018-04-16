node {
    // uncomment these 2 lines and edit the name 'node-6.9.5' according to what you choose in configuration
    def nodeHome = tool name: 'NodeJS', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
    env.PATH = "${nodeHome}/bin:${env.PATH}"

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
        sh "ng test --watch=false --browsers PhantomJS"
    }

    stage('build') {
        sh "ng build --prod --env=dev"
    }

    stage('Archive') {
        sh 'tar -cvzf dist.tar.gz --strip-components=1 dist'
        archive 'dist.tar.gz'
    }

    stage('Deploy') {
        echo "Deploy..."
        sh "rm -rf /usr/share/nginx/html"
        sh "tar -xvzf /var/lib/jenkins/jobs/cds-pipeline/builds/lastStableBuild/archive/dist.tar.gz --strip-components=1 --directory /usr/share/nginx/html"
    }

    stage('Automation') {
        echo "Automation..."
    }
}

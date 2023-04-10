ansiColor('xterm') {
    node {
        stage('Checkout') {
            // Clean the workspace
            cleanWs()
            // Get some code from a GitHub repository
            checkout scm
        }
        stage('Setup') {
            sh "ansible-galaxy install -r requirements.yml"
        }
        stage('Validate') {
            //sh "packer validate jenkins.json"
            sh "packer validate ubuntu-2204-daily.pkr.hcl"
        }
        stage('Run Serva') {
            sh 'C:\\serva\\Serva.exe'
        }
        stage('Build') {
            //withCredentials([usernamePassword(credentialsId: 'aws_access_keys', usernameVariable: 'AWS_ACCESS_KEY', passwordVariable: 'AWS_SECRET_KEY')]) {
            // Run the packer build
            //sh "packer build -var 'aws_region=us-west-2' jenkins.json"
            //}
            sh "packer build ubuntu-2204-daily.pkr.hcl"
        }
        stage('Store Artifacts') {
            archiveArtifacts 'manifest.json'
        }
    }
}
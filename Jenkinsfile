pipeline {
   agent any

   tools {
	   go { 'go-1.14' }
   }

   stages {
      stage('Copy artifact') {
         steps {
            copyArtifacts filter: 'go-artifact', fingerprintArtifacts: true, projectName: 'go-artifact', selector: lastSuccessful()
         }
      }
      stage('Deliver') {
         steps {
            sshagent(['vagrant-toolbox-key']) {
                sh 'scp go-artifact vagrant@10.10.50.3:~'
            }
         }
      }
   }
}

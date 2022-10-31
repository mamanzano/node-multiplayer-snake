node ('ubuntu-app-agent'){  
    def app
    stage('Cloning Git') {
        /* Let's make sure we have the repository cloned to our workspace */
       checkout scm
    }  
    stage('SAST'){
       /* build 'SECURITY-SAST-SNYK' */

	sh 'echo sast stage'
    }

    
    stage('Build-and-Tag') {
    /* This builds the actual image; synonymous to
         * docker build on the command line */
        app = docker.build("mmanzano86/snake")
    }
    stage('Post-to-dockerhub') {
    
     docker.withRegistry('https://registry.hub.docker.com', 'docker_hub_key') {
            app.push("latest")
        			}
         }
    stage('SECURITY-IMAGE-SCANNER'){
       /* build 'SECURITY-IMAGE-SCANNER-AQUAMICROSCANNER' */
	
	sh 'echo scanner stage'
    }
  
    
    stage('Pull-image-server') {
    
         sh "docker-compose down"
         sh "docker-compose up -d"	
    }
    
    stage('DAST'){
       /* build 'SECURITY-DAST-OWASP_ZAP' */
	sh 'echo dast stage'
    }
 
}

node 'prod' {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build images') {
        /* This builds the actual image; synonymous to
         * docker build on the command line. */
             echo "${env.BUILD_NUMBER}"
             sh 'docker build -t linuxcloudops/website-test:${env.BUILD_NUMBER} -f webpage'
    }
    stage('Push Image') {
            withDockerRegistry([ credentialsId: "docker-hub-credentials", url: "" ]){
            echo "${env.BUILD_NUMBER}"
            sh "docker push linuxcloudops/website-test:${env.BUILD_NUMBER}"
           }
   }
    stage('Deploy ') {  
           
           /* sh " docker srevice create --name web -p 9089:80  linuxcloudops/website-test:${env.BUILD_NUMBER}"  */
            /*sh "docker stack deploy -c docker-stack.yml web" */
         }
   }   

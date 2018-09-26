node  ('prod'){
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build images') {
        /* This builds the actual image; synonymous to
         * docker build on the command line. */
             echo "${env.BUILD_NUMBER}"
             sh 'docker build -t linuxcloudops/website-test -f webpage .'
    }
    stage('Push Image') {
            withDockerRegistry([ credentialsId: "ce536e2b-59f1-48a2-bb89-384f0c5a5c2e", url: "" ]){
            echo "${env.BUILD_NUMBER}"
            sh "docker tag linuxcloudops/website-test linuxcloudops/website-test:${env.BUILD_NUMBER}"
            sh "docker push linuxcloudops/website-test:${env.BUILD_NUMBER}"
           }
   }
    stage('Deploy ') {  
           
           /* sh " docker srevice create --name web -p 9089:80  linuxcloudops/website-test:${env.BUILD_NUMBER}"  */
             echo "linuxcloudops/website-test:${env.BUILD_NUMBER}"
             sh " sed -i 's/linuxcloudops/website-test:/linuxcloudops/website-test:${env.BUILD_NUMBER}/g' docker-stack.yml"
             sh "docker stack deploy -c docker-stack.yml web" 
         }
   }   

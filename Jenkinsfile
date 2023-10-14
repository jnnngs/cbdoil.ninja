node (agent){
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */
        dir("app") {
            sh 'docker image build --no-cache -t gilsteadprivatehire .'
        }
    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        sh 'docker tag gilsteadprivatehire:latest reg.jnnn.gs/gilsteadprivatehire:latest'
        sh 'docker login --username=sysad --password=sysad reg.jnnn.gs'
        sh 'docker push reg.jnnn.gs/gilsteadprivatehire:latest' 
    }

    stage('Test HTTP Request') {
        def response = httpRequest "http://httpbin.org/response-headers?param1=123"
        println("Status: ${response.status}")
        println("Response: ${response.content}")
        println("Headers: ${response.headers}")
    }
}

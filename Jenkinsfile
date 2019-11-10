#!groovy
//
//Set Pod Templates for the Java build
podTemplate(cloud: "kubernetes", containers: [
    //Use Alpine where possible
    containerTemplate(name: 'jnlp', image: 'jenkinsci/jnlp-slave:alpine', ttyEnabled: true, alwaysPullImage: true)
]) {
    node(POD_LABEL) {
        //Checkout code from GitHub
        stage ('Checkout') {
            try {
                git credentialsId: 'github-key', branch: "$BRANCH_NAME", url: "git@github.com:bicatana/demo-java.git"
            }
            catch (exc) {
                println "Failed the Git Checkout - ${currentBuild.fullDisplayName}"
            }
        }
        //Ensure that the Workspace is ready for the pipeline
        stage('Check Workspace') {
            container('jnlp'){
                try {
                    sh "ls -la"
                    sh "mkdir test"
                    sh "ls -la"
                    sh "echo 'It works!!!!!'"
                }
                catch (exc) {
                    println "Failed the Workspace Check - ${currentBuild.fullDisplayName}"
                    throw(exc)
                }
            }
        }
    }
}
pipeline {
    stage 'contact docker slave'
    node("docker") {
	    docker.withRegistry('192.168.180.22:32031') {
	        stage 'clone code'
	        git url: "https://github.com/ryandarby/sample/"
	    
	        sh "git rev-parse HEAD > .git/commit-id"
	        def commit_id = readFile('.git/commit-id').trim()
	        println commit_id
	    
	        stage "build"
	        def app = docker.build "sample"
	    
	        stage "publish"
	        app.push 'master'
	        app.push "${commit_id}"
	    }
	}
}

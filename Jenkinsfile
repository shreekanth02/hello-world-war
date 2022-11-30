pipeline {
	agent none
        stages {
           stage ("tomcat buid & move to other node") {
	       agent {label "slv"}
              steps {
                      sh 'sudo mvn package'
		      sh 'ls'
		      sh 'scp -R target/hello-world-war-1.0.0.war jen@172.31.12.113:/opt/tomcat/webapps'
		      echo "sucessfully copied build to other node"
	      }
	   }
	   stage ('diploy in node2') {
	      agent {label "tom"}
	   	steps {
		    sh 'sudo sh /opt/tomcat/bin/shutdown.sh'                   
                    sh 'sudo sleep 3'
                    sh 'sudo sh /opt/tomcat/bin/startup.sh'
                    echo "diployment is sucessfull"
                    echo "copy the public ip of instace and open it in browser with port:8090"
		}
	   } 	   
        }
}

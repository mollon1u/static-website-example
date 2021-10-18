pipeline{
     environment {
       IMAGE_NAME = "website"
       IMAGE_TAG = "latest"
     }
    agent none
    stages {
        stage("build"){
	    agent any
            steps {
                sh """
                    docker build -t $IMAGE_NAME:$IMAGE_TAG  .
                """
            }
        }
        stage("run"){
	    agent any
            steps{
                sh """
		    docker stop $IMAGE_NAME 
		    docker rm $IMAGE_NAME 
                    docker run --name $IMAGE_NAME -d -p 8000:80 -e PORT=80 $IMAGE_NAME:$IMAGE_TAG
		    sleep 5
                """
            }
        }
       stage('Test image') {
           agent any
           steps {
              script {
                sh '''
                    curl http://3.238.6.181/ | grep -q Dimension 
                '''
              }
           }
	}
    }
}
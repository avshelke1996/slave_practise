pipeline{
    agent{
        label{
            label "slave-2"
            customWorkspace "/mnt/slaave-2"
        }
    }
    stages{
        stage("clean"){
            steps{
                echo "clean"
                
                sh '''
                CONTAINERS=$(sudo docker ps -q)
                echo "+++++++++++++++${CONTAINERS}"
                if [ -n "${CONTAINERS}" ]
                then
                    sudo docker stop ${CONTAINERS} && sudo docker rm ${CONTAINERS}
                else
                    echo "no running container"
                fi
                '''
               
            }
        }
        stage("build"){
            steps{
                echo "build"
                sh "sudo chmod 777 index.html"
                sh "sudo docker run -dp 60:80 --name s3 httpd"
                sh "sudo docker cp index.html s3:/usr/local/apache2/htdocs"
            }
        }
        stage("deploy"){
            steps{
                echo "deploy"
            }
        }
    }
}

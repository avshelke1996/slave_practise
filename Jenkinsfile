pipeline{
    agent{
        label{
            label "built-in"
            customWorkspace "/mnt/mainbranch"
        }
    }
    stages{
        stage("clean"){
            steps{
                echo "clean"
                
                sh '''
                CONTAINERS=$(docker ps -q)
                echo "+++++++++++++++${CONTAINERS}"
                if [ -n "${CONTAINERS}" ]
                then
                    docker stop ${CONTAINERS} && docker rm ${CONTAINERS}
                else
                    echo "no running container"
                fi
                '''
               
            }
        }
        stage("build"){
            steps{
                echo "build"
                sh "chmod 777 index.html"
                sh "docker run -dp 60:80 --name s3 httpd"
                sh "docker cp index.html s3:/usr/local/apache2/htdocs"
            }
        }
        stage("deploy"){
            steps{
                echo "deploy"
            }
        }
    }
}

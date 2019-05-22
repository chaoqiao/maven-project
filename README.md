# simple-maven-webapp
#
#  Pipeline Workflow
#  1. Jenkins fetch maven project code
#  2. Jenkins build the code to war file
#  3. Jenkins download tomcat image then rebuild the image, copy the war file to webapp directory and rename to web 
#  4. Jenkins push new image to dockerhub
#  5. Jenkins use ssh agent plugin to excute command on remote server to run container.
#
#  Note: 
#  1. need to configure two login details in Jenkins credentials, DockerHub, Remote Server Login
#  2. need to configure the  JAVA_HOME in Global Configuration
#  3. need to configure the Maven tools in Global Tools Configuration
#  4. need to configure install ssh agent plugin in Jenkins
#

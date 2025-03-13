# Jenkins Installation and Setup on Google Cloud VM
Prerequisites
- A virtual machine (VM) on Google Cloud
- Ubuntu OS installed on the VM
- Docker installed on the VM

Step 1: Install Docker
Step 2: Pull and Run Jenkins Image
# Pull the official Jenkins image from Docker Hub
docker pull jenkins/jenkins
# Run the Jenkins container
docker run jenkins/jenkins
# Verify that the Jenkins container is running
docker ps
docker ps -a

Step 3: Find Your VM's Internal IP. To access Jenkins internally, find your VM's internal IP:
docker inspect <container-id>
# If using VMware, access Jenkins via http://internal-ip:8080.

Step 4: Configure Jenkins for Public Access
If using a cloud server, configure it to allow public access to Jenkins:
# Open port 8080 in the firewall settings of your cloud provider.

docker run -p 8080:8080 jenkins/jenkins
# Find your public IP address and access Jenkins via http://public-ip:8080.

Step 5: Enable Persistent Storage for Jenkins
By default, all Jenkins data (plugins, jobs, configurations) is stored in /var/jenkins_home inside the container. If the container is removed, the data is lost.
# Create a directory for Jenkins data on the host machine
mkdir /root/my-jenkins-data
# We mount a volume (-v /root/my-jenkins-data:/var/jenkins_home) for data persistence.
docker run -p 8080:8080 -v /root/my-jenkins-data:/var/jenkins_home jenkins/jenkins

(Optional) Run Jenkins as root if have permission issue. 
docker run -p 8080:8080 -v /root/my-jenkins-data:/var/jenkins_home -u root jenkins/jenkins

Accessing Jenkins
Once the container is running, access Jenkins by navigating to:
http://<your-public-ip>:8080

Conclusion
You have successfully set up a Jenkins web server on a Google Cloud VM using Docker. Jenkins data is now persistent, and you can access the web interface via your public IP.


# References
https://www.jenkins.io/blog/2018/12/10/the-official-Docker-image/
https://hub.docker.com/r/jenkins/jenkins/

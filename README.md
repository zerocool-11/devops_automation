### here's the code for creating jenkins image

FROM ubuntu
RUN apt update

RUN apt install -y wget

RUN apt-get install -y gnupg2

RUN bash -c "wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | apt-key add -"

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 9B7D32F2D50582E6

RUN echo "deb http://pkg.jenkins.io/debian-stable binary/" > /etc/apt/sources.list.d/jenkins.list

RUN apt update

RUN apt install -y openjdk-8-jdk

RUN apt install -y jenkins

RUN apt install -y net-tools

RUN apt install -y sudo

RUN echo -n "jenkins     ALL=(ALL:ALL)   NOPASSWD: ALL" >> /etc/sudoers

CMD service jenkins start  && bash

EXPOSE 8080


# after this simply run docker run command with jenkins image



# in this job1 we copied the code from github using pollscm
# so that whenever dev push it will clone and copied to jenkins

# build_shell

sudo cp * /mnt   (note - i already mounted my host folder with /mnt folder if jenkin so that whenever something get copied it will added to my host folder   )

In the second job_2 i launched a new docker container for testing if its not there    after job_1 completed successfully

# build_shell code:

if sudo docker ps| grep test

then

echo "its running"

else

sudo docker run -dit --name test -v /home/zerocool/Desktop/jenkins_data:/var/www/html bitbull/webserver

fi


# note :- before this you have to mount one more file with your jenkins container i.e.  /var/run/docker.sock:/var/run/docker.sock

# so that you can launch container inside of container  but before this install docker in that container


# Now, job_3 is for testing and mailing here i used curl for testing and if its response is 200 then it means its working fine  
# otherwise exit 1

# here's the shell code:

#!/bin/bash

if [[ $(sudo curl  -s -w "%{http_code}" http://172.17.0.4/ -o /dev/null) == 200 ]]

then

exit 0

else

exit 1

fi


# and after this in the post build action select mail notification  and configure mail in jenkins setting

# then you'll get mail everytime whenever job3 fails

# and there is also a job 4 to check if the testing container crash then it will restart



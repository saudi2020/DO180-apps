
# start from rhel 7.2
FROM docker.io/centos:7


# update OS
RUN yum -y update && \
yum -y install sudo openssh-clients telnet unzip java-1.8.0-openjdk-devel && \
yum clean all

# enabling sudo group
# enabling sudo over ssh
RUN echo '%wheel ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers && \
sed -i 's/.*requiretty$/Defaults !requiretty/' /etc/sudoers

# add a user for the application, with sudo permissions
RUN useradd -m jboss ; echo jboss: | chpasswd ; usermod -a -G wheel jboss

# Change the user to root user
USER root

# Create a directory /opt/jboss
RUN mkdir -p /opt/jboss

# change workdir to be /opt/jboss
WORKDIR /opt/jboss
 
# copy  jboss-eap-7.2.0.zip to /opt/jboss
ADD jboss-eap-7.2.0.zip /opt/jboss
 
# Unzip /opt/jboss/jboss-eap-7.2.0.zip
RUN unzip /opt/jboss/jboss-eap-7.2.0.zip 
 
#create env JBOSS_HOME=/opt/jboss/jboss-eap-7.2
ENV JBOSS_HOME=/opt/jboss/jboss-eap-7.2
 
# run script $JBOSS_HOME/bin/add-user.sh admin Admin#70365 --silent
RUN $JBOSS_HOME/bin/add-user.sh admin Admin#70365 --silent
 
# user jboss
USER jboss

EXPOSE 8080 9990 9999
 
CMD ["/opt/jboss/jboss-eap-7.2/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0"]

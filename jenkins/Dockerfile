FROM jenkins/jenkins:lts
# if we want to install via apt
USER root
RUN apt-get update && apt-get install -y apt-utils curl vim nano telnet net-tools acl
#RUN apt-get install -y cron
#COPY crontab /etc/cron.d/cjob
#RUN  chmod 0644 /etc/cron.d/cjob
ENV  M2_HOME=/var/jenkins_home/apache-maven-3.5.4
ENV  M2=$M2_HOME/bin
ENV  PATH=$M2:$PATH
#RUN  chown -R jenkins:jenkins /etc/hosts 
#RUN setfacl -Rm u:jenkins:rwx /etc
#CMD ["setfacl", "-Rm", "u:jenkins:rwx", "/etc/hosts"]

RUN chown jenkins /etc/hosts

RUN curl -sSL https://get.docker.com/ | sh

RUN usermod -a -G staff,docker jenkins


# drop back to the regular jenkins user - good practice

COPY builds/spring-data-elasticsearch-3.0.10.BUILD-SNAPSHOT.jar /spring-data-elasticsearch-3.0.10.BUILD-SNAPSHOT.jar
#COPY builds/settings.xml /settings.xml
COPY builds/spring-data-elasticsearch-3.0.10.build-snapshot.pom /spring-data-elasticsearch-3.0.10.build-snapshot.pom
COPY entry.sh /entry.sh
#COPY builds/docker-entrypoint.sh /docker-entrypoint.sh

COPY --chown=jenkins:jenkins builds/docker-entrypoint.sh /docker-entrypoint.sh
RUN ["chmod", "+x", "/docker-entrypoint.sh"]
RUN ["/bin/sh", "-c" , "/docker-entrypoint.sh"]
#CMD cron -f
#ENTRYPOINT ["/bin/sh", "-c" , "/docker-entrypoint.sh" ]

USER jenkins
ENTRYPOINT ["/bin/sh", "-c" , "/docker-entrypoint.sh" ]

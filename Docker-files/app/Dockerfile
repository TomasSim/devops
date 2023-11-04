FROM openjdk:11 as BUILD_IMAGE
RUN apt update && apt install maven -y
RUN git clone https://github.com/TomasSim/devops.git
RUN cd devops && git checkout docker && mvn install

FROM tomcat:9-jre11
LABEL "Project"="VProfile"
LABEL "Author"="Tomas"
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE devops/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
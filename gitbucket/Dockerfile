FROM openjdk:11-jre

ENV GITBUCKET_VERSION=4.38.4

ADD https://github.com/gitbucket/gitbucket/releases/download/${GITBUCKET_VERSION}/gitbucket.war /opt/gitbucket.war

RUN ln -s /gitbucket /root/.gitbucket

VOLUME /gitbucket

EXPOSE 8080 29418

CMD ["sh", "-c", "java -jar /opt/gitbucket.war"]

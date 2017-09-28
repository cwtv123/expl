FROM kk98kk0/tomcat:9.0

RUN set -ex \
    && rm -rf /usr/local/tomcat/webapps/* \
    && chmod a+x /usr/local/tomcat/bin/*.sh

COPY S2-045.war /usr/local/tomcat/webapps/ROOT.war
EXPOSE 8080

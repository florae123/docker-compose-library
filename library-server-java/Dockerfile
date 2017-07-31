#FROM registry.ng.bluemix.net/ibmliberty
FROM websphere-liberty:javaee7
COPY target/library-server-java.war /opt/ibm/wlp/usr/servers/defaultServer/dropins/
EXPOSE 9080
#database credentials
ENV username=f1054f74-38f7-4654-b982-1af0b9b1c717-bluemix
ENV password=34cd6201661e9bd02a10bc048a51ea68d9e25d1a16fea1a88ba14d5f6ef0183c

# 1 if using cloudant-developer in docker container, anything else, if not
ENV CLOUDANT_DEVELOPER=1


CMD ["/opt/ibm/wlp/bin/server", "run", "defaultServer"]

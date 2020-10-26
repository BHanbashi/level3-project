FROM maven:3-jdk-11 as build

WORKDIR /tmp
copy src /tmp/src
copy pom.xml /tmp/

RUN mvn clean package


from adoptopenjdk/openjdk11:alpine

COPY --from=build /tmp/target/queue-master.jar /queue-master.jar
run chmod a+rx ./queue-master.jar


LABEL org.label-schema.vendor="bhanbashi" \
  org.label-schema.name="Socks Shop: queue-master" \
  org.label-schema.description="REST API for queue-master service" \
  org.label-schema.url="https://github.com/microservices-demo/queue-master.git" \
  org.label-schema.vcs-url="github.com:microservices-demo/queue-master.git" \
  org.label-schema.schema-version="1.0"

ENTRYPOINT ["/opt/java/openjdk/bin/java","-jar","./queue-master.jar", "--port=8080"]


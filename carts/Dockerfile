FROM maven:3-jdk-11 as build

WORKDIR /tmp
copy src /tmp/src
copy pom.xml /tmp/

RUN mvn clean package


from adoptopenjdk/openjdk11:alpine

COPY --from=build /tmp/target/carts.jar /carts.jar
run chmod a+rx ./carts.jar


LABEL org.label-schema.vendor="bhanbashi" \
  org.label-schema.name="Socks Shop: carts" \
  org.label-schema.description="REST API for carts service" \
  org.label-schema.url="https://github.com/microservices-demo/carts.git" \
  org.label-schema.vcs-url="github.com:microservices-demo/carts.git" \
  org.label-schema.schema-version="1.0"

ENTRYPOINT ["/opt/java/openjdk/bin/java","-jar","./carts.jar", "--port=80"]

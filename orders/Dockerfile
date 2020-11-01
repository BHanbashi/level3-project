FROM maven:3-jdk-11 as build

WORKDIR /tmp
copy src /tmp/src
copy pom.xml /tmp/

RUN mvn clean package


from adoptopenjdk/openjdk11:alpine

COPY --from=build "/tmp/target/*.jar" ./orders.jar
run chmod a+rx ./orders.jar


LABEL org.label-schema.vendor="bhanbashi" \
  org.label-schema.name="Socks Shop: orders" \
  org.label-schema.description="REST API for orders service" \
  org.label-schema.url="https://github.com/microservices-demo/orders.git" \
  org.label-schema.vcs-url="github.com:microservices-demo/orders.git" \
  org.label-schema.vcs-ref="${COMMIT}" \
  org.label-schema.schema-version="1.0"

ENTRYPOINT ["java","-Djava.security.egd=file:/dev/urandom","-jar","./orders.jar", "--port=80"]


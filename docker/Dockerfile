FROM bitnami/git:latest AS stage1
WORKDIR /repo
ARG REPO_URL=https://github.com/Veena-devops/Ekart.git
RUN git clone $REPO_URL /repo
CMD ["bash"]

FROM maven:amazoncorretto AS stage2
WORKDIR /build
COPY --from=stage1 /repo/src /build/src
COPY --from=stage1 /repo/pom.xml /build/pom.xml
RUN mvn clean package -DskipTests=true
CMD ["bash"]

FROM openjdk:8u151-jdk-alpine3.7
EXPOSE 8070
ENV app /usr/src/app
COPY --from=stage2 /build/target/shopping-cart-0.0.1-SNAPSHOT.jar $app/app.jar
WORKDIR $app
ENTRYPOINT ["sh", "-c", "java -jar app.jar && tail -f /dev/null"]

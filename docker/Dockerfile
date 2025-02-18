FROM maven AS maven
WORKDIR /build
COPY . .
RUN mvn clean package

FROM openjdk:8u151-jdk-alpine3.7
EXPOSE 8070
ENV APP_HOME /usr/src/app
COPY --from=maven /build/target/shopping-cart-0.0.1-SNAPSHOT.jar $APP_HOME/app.jar
WORKDIR $APP_HOME
ENTRYPOINT exec java -jar app.jar

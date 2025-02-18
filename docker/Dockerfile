FROM maven AS maven
WORKDIR /app
COPY /Ekart/src /app/src
COPY /Ekart/pom.xml /app/pom.xml
RUN mvn clean package
CMD ["bash"] 

FROM openjdk:8u151-jdk-alpine3.7
EXPOSE 8070
ENV APP_HOME /usr/src/app
COPY --from=maven /app/target/shopping-cart-0.0.1-SNAPSHOT.jar $APP_HOME/app.jar
WORKDIR $APP_HOME
ENTRYPOINT exec java -jar app.jar

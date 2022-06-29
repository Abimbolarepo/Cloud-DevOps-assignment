FROM openjdk:slim-bullseye
WORKDIR /app
COPY . .
RUN chmod +x mvnw
RUN apt update && apt install -y nodejs npm && \
    ./mvnw clean verify && chmod a+x start.sh
#COPY target/react-and-spring-data-rest-*.jar /app
EXPOSE 8080
CMD ["bash", "-c", "/app/start.sh;"]
FROM maven:3.9.11-eclipse-temurin-25-noble AS build
ADD . /app
WORKDIR /app    
RUN mvn package 

FROM eclipse-temurin:25.0.1_8-jdk-noble AS runtime
LABEL javaproj=spc
LABEL author=anusha
LABEL env=prod
ENV JAVA_HOME=/usr/lib/jvm/openjdk-25-jdk-amd64/bin 
ENV MAVEN_HOME=/usr/share/maven
ARG usrname=devops
RUN useradd -m -d /usr/share/${usrname} -s /bin/bash ${usrname}
USER ${usrname}
WORKDIR /home/novbatch
COPY --from=build /app/target/*.jar anusha.jar
EXPOSE 8080
CMD ["java","-jar","anusha.jar"]
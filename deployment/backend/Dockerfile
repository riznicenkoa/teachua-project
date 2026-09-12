FROM maven:3.9-eclipse-temurin-17 AS build

WORKDIR /app
COPY pom.xml .
RUN mvn -B -q dependency:go-offline
COPY src ./
RUN mvn -B -q clean package -DskipTests


FROM eclipse-temurin:17-jre

WORKDIR /app
COPY --from=build /app/target/*.war /app.war

EXPOSE 8080

ENTRYPOINT ["sh","-c","exec java $JAVA_OPTS -jar /app.war"]

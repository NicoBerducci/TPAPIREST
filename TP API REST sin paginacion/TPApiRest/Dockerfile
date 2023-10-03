# Etapa de construcción
FROM alpine:latest as build

RUN apk update
RUN apk add openjdk17

WORKDIR /app

# Copia los archivos desde el directorio del proyecto
COPY ./TPAPIREST/TP API REST sin paginacion/TPApiRest/.

RUN chmod +x ./gradlew
RUN ./gradlew bootJar --no-daemon

# Etapa de producción
FROM openjdk:17-alpine

EXPOSE 9000

WORKDIR /app

# Copia el archivo JAR construido desde la etapa anterior al contenedor
COPY --from=build /app/build/libs/TPApiRest-0.0.1-SNAPSHOT.jar /app/app.jar

ENTRYPOINT ["java", "-jar", "/app/app.jar"]

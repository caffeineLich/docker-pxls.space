# Force Build 8
FROM maven:3.9-eclipse-temurin-17 AS build

RUN java -version
WORKDIR /Pxls
RUN git clone https://github.com/pxlsspace/Pxls.git .;
RUN mvn clean package; \
    mkdir /tmp/pxls; \
    cp target/pxls*.jar /tmp/pxls/pxls.jar; \
    cp -r resources/* /tmp/pxls

FROM eclipse-temurin:17-jdk-alpine
RUN apk add\ 
	curl
LABEL maintainer="Aneurin Price adp@nyeprice.space"
COPY --from=build /tmp/pxls /tmp/
COPY entrypoint.d/ /entrypoint.d
HEALTHCHECK CMD curl --fail http://localhost:4567/ || exit 1
ENTRYPOINT [ "/bin/run-parts", "--exit-on-error", "/entrypoint.d" ]

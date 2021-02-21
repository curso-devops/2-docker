FROM nginx:alpine

# Install java 8
RUN apk -U add openjdk8 \
    && rm -rf /var/cache/apk/*;
RUN apk add ttf-dejavu

# Install java microservice
ENV JAVA_OPTS=""
ARG JAR_FILE
ADD ${JAR_FILE} app.jar

# Install app on nginx serve
# Use a volume is more efficient and speed than filesystem
VOLUME /tmp
RUN rm -rf /usr/share/nginx/html/*
COPY nginx.conf /etc/nginx/nginx.conf
COPY dist/billingApp /usr/share/nginx/html
COPY appshell.sh appshell.sh

# Expose port 8080 for java swagger and port 80 for ngingx app
EXPOSE 80 8080
ENTRYPOINT ["sh", "/appshell.sh"]
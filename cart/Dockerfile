FROM node:20.19.5-alpine AS build
WORKDIR /opt/server
COPY package.json .
COPY *.js .
RUN npm install

FROM node:20.19.5-alpine 
WORKDIR /opt/server
RUN  addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/server
EXPOSE 8080
LABEL com.project="roboshop" \
      component="cart" \
      created_by="poojithkumar"
COPY --from=build  --chown roboshop:roboshop /opt/server /opt/server
ENV REDIS_URL="redis://redis:6379" \
    CATALOGUE_HOST="catalogue" \
    CATALOGUE_PORT="8080"
USER roboshop
CMD ["server.js"]
ENTRYPOINT ["node"]
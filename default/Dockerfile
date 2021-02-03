FROM node:lts-alpine as controllerbuild
ARG TAG=next
RUN apk add --no-cache git python build-base linux-headers udev
WORKDIR /app
RUN npx degit tagyoureit/nodejs-poolController#${TAG}
RUN npm ci
RUN npm run build-prod


FROM node:current as releasecontainer
COPY --from=controllerbuild /app/dist/compiled /app
WORKDIR /app
EXPOSE 4200
ENTRYPOINT ["node", "/app/index.js"] 

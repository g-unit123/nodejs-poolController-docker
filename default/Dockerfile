FROM node:lts-alpine AS build
ARG TAG=next
RUN apk add --no-cache make gcc g++ python linux-headers udev tzdata git
WORKDIR /app
RUN npx degit tagyoureit/nodejs-poolController#${TAG}
#RUN npm install
#RUN npm run build && npm prune --production
RUN npm ci
RUN npm run build
RUN ci --production

FROM node:lts-alpine as prod
#RUN mkdir /app && chown node:node /app
RUN mkdir /app && chown node:node /app && mkdir /app/data && chown node:node /app/data
WORKDIR /app
COPY --chown=node:node --from=build /app .
#COPY --chown=node:node --from=build /app/node_modules ./node_modules
#COPY --chown=node:node --from=build /app/defaultConfig.json /app/package.json ./
#COPY --chown=node:node --from=build /app/dist ./dist
#COPY --chown=node:node --from=build /app/logger ./logger
#COPY --chown=node:node --from=build /app/web ./web
#RUN mkdir /app/config_file
#RUN cp /app/defaultConfig.json /app/config_file/config.json
#RUN ln -s /app/config_file/config.json /app/config.json
USER node
ENV NODE_ENV=production
ENTRYPOINT ["node", "dist/app.js"]

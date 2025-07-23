FROM node:lts-slim as runtime

WORKDIR /app


COPY package*.json ./


RUN npm install npm -g


RUN npm init -y


RUN npm install -f


COPY . .


RUN npm run build


EXPOSE 3001


CMD [ "npx", "serve", "-s", "build" ]

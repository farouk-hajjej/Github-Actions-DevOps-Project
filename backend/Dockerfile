FROM node:20

WORKDIR /app

COPY package*.json ./ 
RUN npm install npm -g
RUN npm init -y

RUN npm install -f

COPY . .

EXPOSE 3000 

CMD [ "npm","start" ]
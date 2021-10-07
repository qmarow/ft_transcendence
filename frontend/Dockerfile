FROM node:14.17.5-alpine

WORKDIR /usr/src/app/frontend

COPY package*.json ./

RUN npm install

COPY . .

# RUN npm run build

# RUN npm install -g serve

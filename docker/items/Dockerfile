FROM node:20-alpine

WORKDIR /app

COPY app/backend/items/package*.json ./

RUN npm install

COPY app/backend/items .

EXPOSE 3003

CMD ["node", "server.js"]
FROM node:20-alpine

WORKDIR /app

COPY app/backend/discounts/package*.json ./

RUN npm install

COPY app/backend/discounts .

EXPOSE 3002

CMD ["node", "server.js"]
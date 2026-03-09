FROM node:20-alpine

WORKDIR /app

COPY app/backend/auth/package*.json ./

RUN npm install

COPY app/backend/auth .

EXPOSE 3001

CMD ["node", "server.js"]
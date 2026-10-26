# Backend Dockerfile for Express App
FROM node:18-alpine
# Will require Node and packages installed with npm install.
WORKDIR /app
# Entrypoint of express app is `node index.js` 
COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 5000

CMD ["node", "index.js"]

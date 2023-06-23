FROM node:12.22.12
WORKDIR /app
COPY package*.json ./
RUN npm i
COPY index.js index.js
CMD ["node", "index.js"]
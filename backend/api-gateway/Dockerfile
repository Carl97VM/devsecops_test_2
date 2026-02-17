FROM node:20-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci --omit=dev --ignore-scripts && \
    npm install cross-spawn@7.0.6 glob@10.5.0 tar@7.5.7 --save-exact --omit=dev && \
    npm cache clean --force

COPY . .

USER node

EXPOSE 3000
CMD ["node", "src/server.js"]

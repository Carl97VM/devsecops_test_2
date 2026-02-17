FROM node:20-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci --omit=dev --ignore-scripts && \
    npm audit fix --force --omit=dev || true

COPY . .

USER node

EXPOSE 3001
CMD ["node", "src/server.js"]
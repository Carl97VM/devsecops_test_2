FROM node:20-alpine

WORKDIR /app

COPY package*.json ./
RUN sed -i 's/"cross-spawn": "7.0.3"/"cross-spawn": "7.0.6"/g' package.json && \
    sed -i 's/"glob": "10.4.2"/"glob": "10.5.0"/g' package.json && \
    sed -i 's/"tar": "6.2.1"/"tar": "7.5.7"/g' package.json

# 3. Instalación limpia
RUN npm ci --omit=dev --ignore-scripts

COPY . .

USER node

EXPOSE 3002
CMD ["node", "src/server.js"]

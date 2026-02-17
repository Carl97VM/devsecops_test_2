FROM node:20-alpine

WORKDIR /app

COPY package*.json ./
# --- EVIDENCIA ANTES DEL PARCHE ---
RUN echo "--- ANTES DEL SED ---" && grep -E "cross-spawn|glob|tar" package.json

# PARCHE QUIRÚRGICO (Ajustado para ser más flexible con los carácteres)
RUN sed -i 's/"cross-spawn": *"[^"]*"/"cross-spawn": "7.0.6"/g' package.json && \
    sed -i 's/"glob": *"[^"]*"/"glob": "10.5.0"/g' package.json && \
    sed -i 's/"tar": *"[^"]*"/"tar": "7.5.7"/g' package.json

# --- EVIDENCIA DESPUÉS DEL PARCHE ---
RUN echo "--- DESPUÉS DEL SED ---" && grep -E "cross-spawn|glob|tar" package.json

# Instalación
RUN npm ci --omit=dev --ignore-scripts

COPY . .

USER node

EXPOSE 3000
CMD ["node", "src/server.js"]

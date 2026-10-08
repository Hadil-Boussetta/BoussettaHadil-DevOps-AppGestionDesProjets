FROM node:22-alpine

WORKDIR /app

COPY package*.json ./

RUN npm ci \
    --fetch-retries=5 \
    --fetch-timeout=300000 \
    --fetch-retry-mintimeout=20000 \
    --fetch-retry-maxtimeout=120000

COPY . .

EXPOSE 4200

CMD ["npm", "start", "--", "--host", "0.0.0.0"]

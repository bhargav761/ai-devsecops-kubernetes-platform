FROM node:14-alpine

WORKDIR /app

ENV NODE_OPTIONS=""
ENV PATH=/app/node_modules/.bin:$PATH

COPY package.json package-lock.json ./

RUN npm install --legacy-peer-deps --no-audit --no-fund

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
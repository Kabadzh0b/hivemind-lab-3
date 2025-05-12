# Stage 1: build
FROM node:20 AS build
WORKDIR /app

COPY package.json package-lock.json ./
RUN npm ci

COPY . .
RUN npm run build

FROM node:20-alpine AS serve
WORKDIR /app

COPY --from=build /app/dist ./dist
COPY --from=build /app/public/config.json ./dist/config.json

RUN npm install -g serve

EXPOSE 3000
CMD ["serve", "-s", "dist", "-l", "3000"]

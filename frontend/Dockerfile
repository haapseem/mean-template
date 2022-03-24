FROM node:16-alpine as npmi
WORKDIR /app
COPY package.json package.json
COPY package-lock.json package-lock.json
RUN npm install

FROM node:16-alpine as development
RUN apk add chromium
RUN export CHROME_BIN=/usr/bin/chromium-browser
WORKDIR /app
COPY --from=npmi /app /app
CMD ["npm", "run", "start"]

FROM node:16-alpine as build
WORKDIR /app
COPY --from=npmi /app /app
RUN npm run build --prod

FROM nginx:alpine as production
COPY --from=build /app/dist/demo-app /usr/share/nginx/html

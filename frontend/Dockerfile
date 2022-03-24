FROM node:latest as development
WORKDIR /app
COPY . .
RUN npm install
CMD ["npm", "run", "start"]

FROM node:latest as build
WORKDIR /app
COPY --from=development /app /app
RUN npm run build --prod

FROM nginx:alpine as production
COPY --from=build /app/dist/demo-app /usr/share/nginx/html

<<<<<<< HEAD
# Build stage
FROM node:16-alpine AS build

=======
FROM node:16-alpine
>>>>>>> e2ffc23c4da067270d27904b08ff199e4075ba26
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
<<<<<<< HEAD

# Production stage
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 3000
CMD ["nginx", "-g", "daemon off;"]
=======
EXPOSE 3000
CMD [\"npx\", \"serve\", \"-s\", \"build\"]
>>>>>>> e2ffc23c4da067270d27904b08ff199e4075ba26

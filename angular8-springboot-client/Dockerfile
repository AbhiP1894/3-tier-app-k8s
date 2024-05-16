# Build stage
FROM node:20.11.1 AS build

WORKDIR /app

# Copy package.json and package-lock.json separately to leverage Docker cache
COPY package*.json ./

RUN npm install -g @angular/cli@17.3.0
#RUN npm install
RUN npm install -g npm@10.6.0

# Copy the rest of the application
COPY . .
RUN npm install
RUN ng build

# Serve stage
FROM nginx:alpine
WORKDIR /usr/share/nginx/html

# Remove default Nginx static files
RUN rm -rf ./*

# Copy built Angular app from the build stage to Nginx directory
COPY --from=build /app/dist/angular8-springboot-client .

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]


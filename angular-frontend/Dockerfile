# Build stage
FROM node:14-alpine AS build
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Runtime stage
FROM nginx:alpine

# Remove default NGINX config
RUN rm /etc/nginx/conf.d/default.conf

# Copy your custom config
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copy Angular build output
COPY --from=build /usr/src/app/dist/angular-frontend /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]


# # Use official Node.js image as the base image
# FROM node:14-alpine AS build

# # Set the working directory in the container
# WORKDIR /usr/src/app

# # Copy package.json and package-lock.json (if available)
# COPY package*.json ./

# # Install project dependencies
# RUN npm install

# # Copy the rest of the application code
# COPY . .

# # Build the Angular application
# RUN npm run build 

# # Use NGINX as the production server
# FROM nginx:alpine

# # Copy the built artifact from the previous stage to NGINX web server directory
# COPY --from=build /usr/src/app/dist/angular-frontend /usr/share/nginx/html

# # Expose port 80 to the outside world
# EXPOSE 80

# # Start NGINX server when the container starts
# CMD ["nginx", "-g", "daemon off;"]

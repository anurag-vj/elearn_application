# Stage 1: Build Stage
# Use the official Node.js image to build the React application
FROM node:18 AS build

# Set working directory inside the container
WORKDIR /react_build

# Copy all files into the container
COPY . .

# Install dependencies and build the production-ready React app
RUN npm install && npm run build

# Stage 2: Deployment Stage
# Use a lightweight Nginx image to serve the static files
FROM nginx:alpine-slim AS deploy

# Copy the built React files from the build stage to Nginx's default html folder
COPY --from=build /react_build/build /usr/share/nginx/html

# Start Nginx server
CMD ["nginx", "-g", "daemon off;"]

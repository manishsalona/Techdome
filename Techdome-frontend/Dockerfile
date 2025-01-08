# Stage 1: Build the React app
FROM node:18 AS builder

# Set working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json for dependency installation
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application source code
COPY . .

# Build the React app for production
RUN npm run build

# Stage 2: Serve the app using nginx
FROM nginx:1.21

# Copy the build output from the previous stage
COPY --from=builder /app/build /usr/share/nginx/html

# Expose the port nginx will serve on
EXPOSE 80

# Start nginx when the container starts
CMD ["nginx", "-g", "daemon off;"]

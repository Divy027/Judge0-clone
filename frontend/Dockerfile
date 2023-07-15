# Use the official Node.js image as the base image for the builder
FROM node:14 as builder

# Set the working directory in the container
WORKDIR /app/frontend

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the frontend code
COPY . .

# Build the React app
RUN npm run build

# Use a lightweight HTTP server to serve the production build
FROM node:14-alpine
RUN npm install -g http-server

# Set the working directory in the container
WORKDIR /app

# Copy the built React app from the builder stage to the working directory
COPY --from=builder /app/frontend/build ./frontend/build

# Expose the frontend port
EXPOSE 3000

# Start the frontend server
CMD ["http-server", "-p", "3000", "./frontend/build"]

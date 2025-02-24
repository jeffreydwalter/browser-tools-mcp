# Dockerfile for browser-tools-server.
# This Dockerfile builds the Node.js browser tools server from source and runs it in production mode.
FROM node:18-alpine AS builder
WORKDIR /usr/src/app

# Copy the package files and install dependencies.
COPY package.json package-lock.json tsconfig.json ./
RUN npm install

# Copy the source code and build the project.
COPY . .
RUN npm run build

# Use a smaller image for production.
FROM node:18-alpine
WORKDIR /usr/src/app

# Copy the built files from the builder stage.
COPY --from=builder /usr/src/app/dist ./dist
COPY package.json ./
RUN npm install --only=production

# Expose port 3025 for the browser tools server.
EXPOSE 3025

# Start the browser tools server.
CMD ["node", "dist/browser-connector.js"] 
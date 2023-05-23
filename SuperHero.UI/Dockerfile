# Use an official Node.js runtime as a parent image
FROM node:16.10

# Set the working directory to /app
WORKDIR /SuperHero.UI

# Copy the package.json and package-lock.json files to the container
COPY package*.json ./

# Install the dependencies
RUN npm install

# Copy the rest of the application to the container
COPY . .

# Build the application
RUN npm run build --frontappang

# Expose port 4200 for the Angular application
EXPOSE 4200

# Start the Angular application
CMD [ "npm", "run", "start:frontappang" ]

#To Set Names For The Images In Docker
LABEL maintainer="Jason Ishak"
LABEL description="My Angular App"

# Set a custom name for the image
LABEL org.opencontainers.image.title="my-angular-super-hero-image-app"

# Set a custom name for the container
LABEL org.opencontainers.container.title="my-angular-super-hero-container"


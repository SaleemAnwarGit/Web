# Use a base image with Ubuntu
FROM ubuntu:20.04

# Install curl and other dependencies
RUN apt-get update && apt-get install -y \
    curl \
    gnupg \
    build-essential

# Install Node.js (and npm)
RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash - \
    && apt-get install -y nodejs \
    && npm install -g npm@latest

# Install Yarn globally
RUN npm install -g yarn

# Set the working directory
WORKDIR /app

# Optionally, add other setup steps
# COPY package.json yarn.lock ./
# RUN yarn install

# Expose port 3000 for the React app
EXPOSE 3000

# Start a bash shell (for development purposes)
CMD [ "bash" ]

# Specify The Base Image As Builder
FROM node:alpine AS builder

# Provide Maintainer Information
MAINTAINER MohammadHosein Chahardoli <mohammadhoseinchahardoli@gmail.com>

# Specify Working Directory
WORKDIR /app

# Add package.json
COPY ./package.json .

# Download and Install All The Dependencies
RUN ["npm", "install"]

# Add The Application Source Code
COPY ./ ./

# Build The Application
RUN ["npm", "run", "build"]

# Specify The Base Image As Runner
FROM nginx:latest

# Provide Maintainer Information
MAINTAINER MohammadHosein Chahardoli <mohammadhoseinchahardoli@gmail.com>

# Expose The Application Port
EXPOSE 3000

# Copy The Built Version of Application
COPY --from=builder /app/build/ /usr/share/nginx/html/

# Copy The Nginx Configuration File
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf



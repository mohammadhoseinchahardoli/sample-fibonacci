# Specify The Base Image
FROM node:alpine

# Provide Maintainer Information
MAINTAINER MohammadHosein Chahardoli <mohammadhoseinchahardoli@gmail.com>

# Specify Working Directory
WORKDIR /app

# Copy package.json
COPY ./package.json .

# Download and Install All The Dependencies
RUN ["npm", "install"]

# Copy The Application Source File
COPY ./ ./

# Start The Application
CMD ["npm", "run", "start"]

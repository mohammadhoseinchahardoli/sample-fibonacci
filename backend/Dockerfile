# Specify The Base Image
FROM node:alpine

# Provide Maintainer Information
MAINTAINER MohammadHosein Chahardoli <mohammadhoseinchahardoli@gmail.com>

# Specify Working Directory
WORKDIR /app

# Add package.json
COPY ./package.json .

# Download and Install All Dependencies
RUN ["npm", "install"]

# Add Application Source Code
COPY ./ ./

# Build The Application
CMD ["npm", "run", "start"]

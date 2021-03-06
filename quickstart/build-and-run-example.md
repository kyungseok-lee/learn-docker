# Build and run image Example

## Git
```
git clone https://github.com/dockersamples/node-bulletin-board
cd node-bulletin-board/bulletin-board-app
```

## Define a container with Dockerfile
```
# Use the official image as a parent image.
FROM node:current-slim

# Set the working directory.
WORKDIR /usr/src/app

# Copy the file from your host to your current location.
COPY package.json .

# Run the command inside your image filesystem.
RUN npm install

# Inform Docker that the container is listening on the specified port at runtime.
EXPOSE 8080

# Run the specified command within the container.
CMD [ "npm", "start" ]

# Copy the rest of your app's source code from your host to your image filesystem.
COPY . .
```

## Build and test your image
```
docker build --tag bulletinboard:1.0 .
```

## Run your image as a container
```
docker run --publish 8000:8080 --detach --name bb bulletinboard:1.0
```

## Remove
- The --force option removes the running container. If you stop the container running with docker stop bb you do not need to use --force.
```
docker rm --force bb
```
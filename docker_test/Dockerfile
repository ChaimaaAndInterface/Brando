# Use an official Node.js runtime as a parent image
# We use the 'alpine' version as it's very lightweight
FROM node:alpine

# Set the working directory inside the container to /app
WORKDIR /app

# Copy the local 'js' folder (containing your app.js)
# into the container's current working directory (/app)
COPY ./js ./js

# Specify the command to run when the container starts
# This will execute your app.js script using Node
CMD ["node", "js/app.js"]

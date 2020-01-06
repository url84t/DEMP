# Set node version to use as the base
FROM node

# Create app directory
WORKDIR /code


# install dependencies
RUN apt-get update && apt-get upgrade -y 

RUN apt-get install -y libsqlite3-dev \
    git \
    sqlite3 \
    graphicsmagick

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
# COPY package*.json ./
RUN npm install -g gulp-cli
RUN npm link gulp
RUN npm install
RUN gulp build

# If you are building your code for production
# RUN npm ci --only=production

# Bundle app source
# COPY . .

EXPOSE 3000
CMD [ "node", "app.js" ]
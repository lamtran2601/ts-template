FROM node:18-slim

RUN apt-get update && apt-get install -y procps

# Create app directory
WORKDIR /app

# A wildcard is used to ensure both package.json AND package-lock.json are copied
COPY package.json yarn.lock* package-lock.json* pnpm-lock.yaml* ./

# Install app dependencies
RUN --mount=type=cache,target=/root/.yarn YARN_CACHE_FOLDER=/root/.yarn yarn install --frozen-lockfile

# Bundle app source
COPY . .

RUN yarn build

EXPOSE 3000

ENV PORT 3000
# Start the server using the production build
CMD ["node", "server.js"]
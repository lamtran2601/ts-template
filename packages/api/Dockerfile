FROM node:18-slim

RUN apt-get update && apt-get install -y procps

# Create app directory
WORKDIR /app
RUN yarn global add @nestjs/cli
# A wildcard is used to ensure both package.json AND package-lock.json are copied
COPY package.json yarn.lock* package-lock.json* pnpm-lock.yaml* ./

RUN --mount=type=cache,target=/root/.yarn YARN_CACHE_FOLDER=/root/.yarn yarn install --frozen-lockfile

# Bundle app source
COPY . .

RUN yarn run build

EXPOSE 3001

ENV API_PORT 3001

CMD ["yarn", "start:prod"]

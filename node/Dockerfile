ARG NODE_VERSION=${NODE_VERSION:-19-alpine}
FROM node:${NODE_VERSION}

RUN npm install --global pnpm

CMD ["pnpm","run","dev"]
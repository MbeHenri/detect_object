FROM node:18-alpine AS builder

ENV NODE_ENV production
WORKDIR /app

COPY package.json ./
COPY yarn.lock ./

RUN yarn install --frozen-lockfile

COPY . .
RUN yarn build

FROM nginx

COPY --from=builder /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

# handle the future env variable begining by REACT_APP_API_ specify as value of real env variable 
COPY env.sh /docker-entrypoint.d/env.sh
RUN chmod +x /docker-entrypoint.d/env.sh

EXPOSE 80 443

# Start the app
# CMD [ "npm", "start" ]

CMD [ "nginx", "-g", "daemon off;" ]
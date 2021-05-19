# 从dochub上获取构建环境镜像
# node 15.9.0
FROM docker.io/aimeimjj/game_platform_fe_build:latest as build-stage

WORKDIR /app

ADD package.json ./
RUN yarn install

COPY . .

ARG NODE_ENV
ENV NODE_ENV ${NODE_ENV}
RUN npm run build:$NODE_ENV

# # # # nginx 部署
FROM nginx:stable-alpine as production-stage
COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build-stage /app/dist /usr/share/nginx/html/h5

EXPOSE 80
CMD ["nginx","-g","daemon off;"]

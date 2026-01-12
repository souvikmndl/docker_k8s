# Build phase --> AS builder names this phase 'builder' so that we can refer to it in successive builds
FROM node:alpine AS builder 
WORKDIR '/app'
COPY package.json .
RUN npm install 
COPY . . 
RUN npm run build    

# FROM cmds also act as terminators for prev phases/blocks, essentially saying the the prev phase is over 
FROM nginx 
COPY --from=builder /app/build /usr/share/nginx/html 
# /app/build will contain the build files
# this copies over the build files from the builder phase 
# nginx img's start cmd automatically runs the nginx server, so no other start code

# the dev server is powerful, has a lot of code for interacting with our dev changes and all
# the prod server's only task is to serve up the static build files(which also contains the node modules code)
# that is why we are using nginx whose sole purpose here is to serve the static files, so not power hungry
# /app/build /usr/share/nginx/html  is the default location for nginx to serve static files

# docker run -p 8080:80 <img_id> --> 80 is the default port for nginx
# frontend-cicd

## Local Test

### 0. After Clone
```
# Install package
$pnpm i

# Prepair config for docker container in vite.config.js

export default defineConfig({
  plugins: [react()],
  server: {
    host: true,
    port: 8080
}
})

# add to package.json

 "scripts": {
    "start": "vite",


```
### 1. add .dockerignore

```
node_modules/
.gitignore
```
### 2. Create Dockerfile.dev for local test
```
FROM node:alpine

WORKDIR '/app'

COPY package*.json .

RUN npm install

COPY . .

CMD ["npm", "start"]
```

### 2. Buid as local

```
#build images for local test
docker build -f Dockerfile.dev -t frontend-cicd:1.0.0 .

#Check images after build
REPOSITORY                             TAG               IMAGE ID       CREATED          SIZE
frontend-cicd                          1.0.0             cbc71c041ee2   11 seconds ago   337MB

```
*Repository name format as local repo [nameOfImages]  |  as remote repo [dockerhubUsername]/[nameofImages]

### 3. Run as local 


```
# docker run -d -p [externalport]:[internalport] [ImagesId]
docker run -d -p 8080:5173 cbc71c041ee2 // Non interact with container
#OR
docker run -d -it -p 8080:5173 cbc71c041ee2 // Interaction with container

#Verify conainer running

$docker ps -a                               
CONTAINER ID   IMAGE                           COMMAND                  CREATED          STATUS                        PORTS                    NAMES
7dc211d391aa   cbc71c041ee2                    "docker-entrypoint.s…"   3 seconds ago    Exited (1) 2 seconds ago                               vibrant_lederberg


```

* check log if error

```
# docker logs [containerId]
$docker logs 7dc211d391aa 

# Example Error

$docker logs 7dc211d391aa 

npm ERR! Missing script: "start"
npm ERR! 
npm ERR! Did you mean one of these?
npm ERR!     npm star # Mark your favorite packages
npm ERR!     npm stars # View packages marked as favorites
npm ERR! 
npm ERR! To see a list of scripts, run:
npm ERR!   npm run

npm ERR! A complete log of this run can be found in: /root/.npm/_logs/2023-07-14T06_51_57_886Z-debug-0.log

*Delete invalid Images with  / $docker rmi -f cbc71c041ee2  / $docker rmi -f [imagesId]
*Edit package.json then rebuid from step 2 again
```
*Access to container for check somthing / $docker exec -it 751d512b29b0 sh  / $docker exec -it [imageId] [sh/bash/zsh]



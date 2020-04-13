
* Create an angular app.
* Create a file named as nginx.conf in the project directory & write below lines.
    ```
    server {
      listen $PORT default_server;
      location / {
        include  /etc/nginx/mime.types;
        root   /usr/share/nginx/html/;
        index  index.html index.htm;
      }
    }
    ```
    NOTE: This file in needed for us as I will upload this to Heroku. And Heroku assigns a default_server. So I created the port as environment variable.(I am not fully clear about the Heroku part :confused: )
* Next create a Dockerfile in the project directory.
* Write below lines in the dockerfile.(ignore line numbers)
    
    ```
    #Stage 1
    1. FROM node:latest as node
    2. WORKDIR /app
    3. COPY . .
    4. RUN npm install
    5. RUN npm run build --prod
    
    #Stage 2
    6. FROM nginx:alpine
    7. COPY --from=node /app/dist/sadda-adda usr/share/nginx/html
    
    ## server configuration I didn't understand
    8. COPY nginx.conf /etc/nginx/conf.d/default.conf
    
    9. CMD sed -i -e 's/$PORT/'"$PORT"'/g' /etc/nginx/conf.d/default.conf && nginx -g 'daemon off;'
    ```
    CMD1: Pull node docker image and name as node
    CMD2: Create a work directory named as app
    CMD3: Copy everything of my project folder to the app directory.
    CMD4: Install all the dependencies.
    CMD5: Build the angular app for production.
    CMD6: Pull nginx docker image. It will serve our angular app.
    CMD7: Copy all files from our production dist app folder(located in node image) to usr/share/nginx/html which is the serve directory of nginx.
    CMD8: Line 8 & 9 needed as I am going to deploy it to Heroku. This line copy our nginx.conf to nginx's default.conf.
    CMD9: Replace the environment variable PORT in default.conf & last line is must. Because if you add a custom CMD in the Dockerfile, be sure to include -g daemon off; in the CMD in order for nginx to stay in the foreground, so that Docker can track the process properly (otherwise your container will stop immediately after starting)! [Read](https://hub.docker.com/_/nginx)

* Now build the image of our angular app by running the command `docker build --rm -f Dockerfile -t sadda-adda:v1 .` in the terminal.
    > CMD: `--rm` removes any intermediate image. `-f Dockerfile` shows the Dockerfile. `-t sadda-add` gives a tag. You can give your own tag. `.` tells to create the image including everything of the current directory.
* `docker images` command will list out all the images including our recently created 'sadda-adda' image.
* Next we can run the image by executing the command `docker run --env PORT=80 --rm -p 80:80 sadda-adda:v1`
    > CMD: `--env PORT=80` we pass the environment variable PORT as 80. 
* Go to `localhost:80` in the browser, you should see your angular app up & running.
* `docker ps` command shows all the running containers.

### Resource
1. [Video1](https://www.youtube.com/watch?v=etA5xiX5TCA)
2. [Docker Environment Variables](https://docs.docker.com/engine/reference/commandline/run/)
2. [nginx Docker Image](https://hub.docker.com/_/nginx)





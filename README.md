# Blog App

A Blogging App built with Go and PostgreSQL. See the
[final branch](https://github.com/betterstack-community/go-blog/tree/final) for
the updated code with Docker configuration.

**Run**:
- `docker compose up --build`
- `docker compose down`

**Commands**:
- Build docker image: <br> `docker build . -t go-blog` <br>
- or `docker build . -t go-blog:0.1.0` <br> (without a tag docker resets to latest) <br>
- Check new image is in your local image library <br> `docker image ls go-blog` <br>
- Create the network <br> `docker network create go-blog-network` <br>
- Launch the container for the app <br> 
    ```
    docker run \
      --rm \
      --name go-blog-app \
      --publish 8000:8000 \
      --env-file .env \
      --network go-blog-network \
      go-blog
    ```
  
- Launch Caddyfile (redirects traffic to the app) <br>
  ```
  docker run \
   --rm \
   --name go-blog-caddy \
   -p 80:80 \
   -v caddy-config:/config \
   -v caddy-data:/data \
   -v $(pwd)/Caddyfile:/etc/caddy/Caddyfile \
   --network go-blog-network \
   caddy
  ```
**Tutorial**:
[Dockerizing Go Applications: A Step-by-Step Guide](https://betterstack.com/community/guides/scaling-go/dockerize-golang/)

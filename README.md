# Docker - FC Samples

## Nginx and Laravel

### Create images for nginx and laravel

1. Inside **nginx** folder create an image 
`docker build -t <your_prefix>/nginx-laravel:prod . -f Dockerfile.prod`

2. You can also make a push to docker hub
`docker push <your_prefix>/nginx-laravel:prod`

3. Inside **laravel** folder create an image 
`docker build -t <your_prefix>/laravel:prod . -f Dockerfile.prod`

4. You can also make a push to docker hub
`docker push <your_prefix>/laravel:prod`


### Run Nginx as a reverse proxy for laravel framework

1. Create bridge network so the containers can communicate with each other 
`docker network create laranet`

2. Run laravel container exposing **9000** port on `laranet` network
`docker run -d --network laranet --name laravel <your_prefix>/laravel:prod`

3. Run nginx container mapping host **8080** port to container **80** port on `laranet` network
`docker run -d --network laranet --name nginx -p 8080:80 <your_prefix>/nginx-laravel:prod`

4. Test accessing http://localhost:8080 


# Docker Build


## Searching your image from the Registry 
> Registry is a place where all the images are stored.

- There are two ways to search image.
    1. Search from Docker Registry using UI
    2. Search from Docker Registry using CLI


- Search from Docker Registry using UI
    1. Login to Docker Registry
    2. Search for the specified

- Search from Docker Registry using CLI
    1. use docker-cli to search image, use the following command
        ```
        docker search ubuntu


        ```
---
## Search, Pull and Run the Image locally  
> Registry is a place where all the images are stored. We would pull the image and then run the image locally.

- Search the Image using docker CLI
    ```
    docker search nginx
    ```

- Pull the image to your local machine
    ```
    docker pull nginx
    ```

- Check the if the image is in our local image cache
    ```
    docker images
    ```
- Run the Image and Port forward it to a Port
    ```
    docker run nginx -p8080:80
    ```

---
## Building your own custom Pizza
> Build your own custom Image of your favourite Pizza, and access it locally.

- Searching a base image for Pizza
    - Just like how every pizza has a base so has the image also has a base
    ```
    docker search nginx
    ```

- Writting your Recipe / Dockerfile 
    - Just like a Recipe a Dockerfile also contains series of layers and steps to perform a make the final image
    ```
    # Base Image / Taking the Pizza Base
    FROM nginx

    # Adding the Code / Adding the Sauce 
    ADD index.html /usr/share/nginx/html

    # Adding some Asset files / Adding Cheese
    ADD pizza.jpg /usr/share/nginx/html

    # Adding Configuration changes / Adding Topings
    EXPOSE 80
    ```

- Time to Bake AKA Build the Pizza Image
    - Just like pizza will be baked in the same way and image also will be baked / buil

    ```
    docker build -t chrisedrego/pizza .
    ```

- Check if pizza image is build
    ```
    docker images
    ```

- Run the image / Serve the pizza
    ```
    docker run chrisedrego/pizza -p8080:80
    ```
---

## Run Custom Images Dettached and Check the logs
> There are often requirements in which we need to run the images in the detached mode. (background mode) to carry around with other stuff and then check the logs
- Search the image
    ```
    docker search
    ```

- Run the Image (dettached mode)
    ```
    docker run -d -p8080:80 chrisedrego/pizza
    ```

- Check the running container
    ```
    docker ps
    ```

- Check the logs from a container
    ```
    docker log <CONTAINER_ID> / <CONTAINER_NAME>
    ```

## Navigate and Get inside of the Container
> There are often at times while troubleshooting we want to get inside of the container
- Finding the container 
```
docker ps
```

- Shell/Exec into the container
```
docker exec -it <CONTAINER_ID> sh
```

- Use silly commands to feel like SUPER_USER
```
ls -al
cd / 
ls -al
```
> Bonus-Point: Container isnt really an OS but you could see that it has virtualized and now as some sort of a VFS which is layed out (Magic of Docker)

## Using Storage for Docker
> Docker by default is ephmeral, to bring in the persistent storage we have the host machine on which its running
- Searching the image
```
docker images
```

- Run and add the mappings for host storage path
```
docker run -d -p8080:80 -v /repo/personal/just-enough-devops/docker/asset:/usr/share/nginx/html --name new-pizza2 nginx
```
---
## Sharing is Caring: Share your docker file to the rest of the world
> Sharing your dockerimage to the rest of the world using Dockerhub Registry

- Authenticate to dockerhub using CLI
```
docker login -u'USERNAME'
```

- Searching the Images
```
docker images
```

- Pushing the Images
```
docker push chrisedrego/pizza
```

---
## Time to clean up the Pizza
> Its now time to clean up the Pizza image and container

- Find the container 
```
docker ps
```

- Stop the container
```
docker stop
```

- Delete the container
```
docker rm CONTAINER_ID
```

---
## Summary

```
docker search 
docker pull
docker build
docker images
docker run
docker ps
docker exec
docker stop
docker login
docker push
docker rmi
docker rm
```
# Project 0: Warm Up of Docker Containers

## Key Concepts
This project introduces Docker containers, covering:
- Building and running a Python-based container.
- Deploying an Nginx web server using Docker.
- Modifying the default Nginx page by mounting a volume.

## How to Run the Code

### Prerequisites
Ensure you have Docker installed on your system.

### Running the Python Script in Docker
1. Clone the repository.
2. Navigate to the project directory:
   ```sh
   cd project0_CECS327

3. Build docker image

    ```sh
    docker build -t my-python-app .

4. Run the container
    ```sh
    docker run my-python-app

### Running the Nginx Web Server

1. Pull the latest Nginx image:

    ```sh
        docker pull nginx:latest
    ```


2. Run the Nginx container with the default page:

    ```sh
        docker run -d -p 8080:80 --name my-nginx nginx:latest
    ```
3. Open http://localhost:8080 in your browser to view the default Nginx page.

### Switching to Custom Nginx Page

1. Ensure your ``index.html`` file is updated in your project directory.

2. Get the container_id

    ```sh
        docker ps
    ```

3. then manually copy your file into the container
    ```sh
        docker cp index.html <contain_id>:/usr/share/nginx/html/index.html
    ```

4. Then reload the nginx:

    ```sh
        docker exec -it <container_id> nginx -s reload
    ```

5. Open http://localhost:8080 to see your updated custom Nginx page.

### Switching Back to Default Nginx Page

1. Stop and remove the custom Nginx container:

    ```sh 
        docker stop my-nginx
    ```
    ```sh
        docker rm my-nginx
    ```

2. Run a new Nginx container without mounting a custom file:

    ```sh
        docker run -d -p 8080:80 --name my-nginx nginx:latest
    ```

3. Open http://localhost:8080 to see the default Nginx page again.

    ```sh
        docker pull nginx:latest
    ```

4. Run an Nginx container:

    ```sh
        docker run -d -p 8080:80 --name my-nginx nginx:latest
    ```

5. Open http://localhost:8080 in your browser to view the default page.

### Modifying the Default Nginx Page

1. Ensure your ```index.html``` file is updated in the project directory.

2. Stop and remove any existing Nginx container (if running):

    ```sh
        docker ps  # Get the running container ID
        docker stop my-nginx  # Stop the container
        docker rm my-nginx  # Remove the container
    ```

4. Run the container with a volume mount to serve your updated index.html:
    ```sh
        docker run -d -p 8080:80 -v $(pwd)/index.html:/usr/share/nginx/html/index.html --name my-nginx nginx:latest

        docker run -d -p 8080:80 -v $(pwd)/index.html:/usr/share/nginx/html/index.html nginx:latest
    ```

5. Open http://localhost:8080 in your browser to see your updated custom Nginx page.
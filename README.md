# DockerFile

Docker Notes


Dockerfile

# Use the official Node.js image as the base image
FROM node:14

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json to the container
COPY package*.json ./

# Install dependencies
RUN npm install
RUN npm install react-scripts@5.0.0 -g

# Copy the rest of the application code to the container
COPY . .

# Build the production version of the React app
RUN npm run build

# Set environment variable to production
ENV NODE_ENV=production

# Expose the port your React app will run on (if applicable)
EXPOSE 3000

# Start the React app
CMD ["npm", "start"]


.dockerignore
node_modules
build
.dockerignore
Dockerfile
Dockerfile.prod


* Build the Docker image:     Open a terminal, navigate to your React app's root directory where the Dockerfile is located, and run the following command:

		docker build [options] PATH
		docker build -t your-image-name .
	Explanation: Build a Docker image from a Dockerfile located at the specified PATH directory.
	Application: Used to create custom Docker images tailored to your application's requirements.
	Example: Build a Docker image named "my-app-image" from the current directory's Dockerfile:

		docker build -t my-app-image .


* Run the Docker container:  
 	Once the Docker image is built, you can run it as a container using the following command:

		docker run [options] IMAGE [command] [args]
		docker run -d -p 80:3000 your-image-name      #(-d) is detached mode
		docker run your-image-name 

	Explanation: Create and start a new container from the specified IMAGE, optionally executing a 		command inside the container.
	Application: Used to launch applications and services inside isolated containers.
	Example: Run a simple Nginx web server in a container: 		docker run -d -p 80:80 nginx  

* Stop the Docker container: This command gives the container some time to clean up and shut down gracefully.
docker stop [options] CONTAINER [CONTAINER...]
		docker stop container-id
	Explanation: Stop one or more running containers gracefully, allowing them to perform cleanup before exiting.
	Application: Used to gracefully shut down running containers.
	Example: Stop a running container with ID "abc123":
		docker stop abc123

 	If the container doesn't stop within a certain time frame (usually 10 seconds), Docker will forcefully 		terminate it using the SIGKILL signal. You can use the
		docker kill


* The line docker rm container-id is a Docker command that removes a stopped container from the system, freeing up resources.
		docker rm [options] CONTAINER [CONTAINER...]
		docker rm container-id
	Explanation: Remove one or more stopped containers from the system.
	Application: Used to clean up stopped containers and free resources.
	Example: Remove a stopped container with ID "xyz456":
		docker rm xyz456


* docker rmi [options] IMAGE [IMAGE...]:
	Explanation: Remove one or more Docker images from the local system.
	Application: Used to clean up unused images and free up disk space.
	Example: Remove an image named "old-image":

		docker rmi old-image


* The line docker images ls is a Docker command used to list all the images available on the local system.
	Explanation: List all available Docker images on the local system.
	Application: Used to view locally available images and their details.
	Example: List all Docker images:
		docker images [options]
		docker images
		docker images ls


* docker version: Shows information about Docker client and server versions, including build details and installed components.
		docker version  


* docker logs [options] CONTAINER:
	Explanation: View the logs of a running or stopped container.
	Application: Used to check the logs of a container for debugging and troubleshooting.
	Example: View the logs of a running container with ID "log-container":

		docker logs log-container
		docker logs container-id

* docker exec [options] CONTAINER COMMAND [ARG...]:
	Explanation: Run a command inside a running container.
	Application: Used to execute commands directly in a running container.
	Example: Execute a bash shell inside a running container with ID "container-id":

		docker exec -it container-id bash


* List all running containers
		docker ps -a
		docker ps

		docker ps [options]

	Explanation: List all running containers, displaying their ID, names, and basic information.
	Application: Used to monitor running containers and check their status.
	Example: List all running containers:
		docker ps

* docker network [subcommand] [options]:
	Explanation: Manage Docker networks, including creating, inspecting, and removing networks.
	Application: Used to create networks for communication between containers or with the host.
	Example: Create a bridge network named "my-network":

		docker network create my-network


* docker inspect container-id
* docker info
* docker login
* docker tag your-local-image:tag username/repository:tag
* docker push username/repository:tag

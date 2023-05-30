<h2>Issues we face before containerazation
	tech_Lead:your software not working on my system
	dev1:it works on my computer
	tech_Lead:then ship your computer to the customer</h2>
<hr/>

<h2>What is containers?
	container is a software itself that wrap all the part of a code and all its dependencies into a single deployable unit that can be used on different systems and servers.</h2>
<hr/>

<h2>Why do we need containers?
	earlier we used virtualized enviroments in virtual machines which we complete os running inside the host os then,
	some group of people noticed that we don't need to compute full os inside the host os if we are only going to use a part of this virtual os,
	so better to disect the virtualization into layers and share the layers that are not necessarily required to be exclusive to this virtual enviroment,</h2>
<hr/>

<h2>What is docker?
	docker is a tool that helps in developing, building, deploying and executing software in isolation. ti does so by creating a container that completely wraps a software.</h2>
<hr/>

<h2>Docker installation</h2>

	1. sudo apt install docker.io
	2. sudo apt remover docker.io -y

	OR

	1.sudo apt update
	2.sudo apt install apt-transport-http ca-certificates curl software-properties-common
	3.curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
	4.sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
	Now,
	5.sudo apt update
	6.sudo apt install docker-ce

<h2>docker enviroment</h2>

	-docker engine
		docker engine is a set of technologies that allows for creation and management of all docker processes it has 3 major parts to it.
			* docker cli		* docker api 	 * docker daemon
	-docker objects
			--docker images:
					Set of instructions that are used to create containers and execute code inside it.
					1.remove docker images:
						sudo docker rmi imagename
					2.list all images:
						sudo docker images
			--docker containers:
					# Commands
					1.pull:
						docker pull ubuntu
					2.list all images:
						sudo docker images
					3.run a container into a interactive detached mode with terminal:
						sudo docker run -it -d ubuntu
					4.list all containers:
						sudo docker ps -a
					5.add name to your container(default:docker will assign random name to your container) with port exposed:
						sudo docker run -it -d --name mycontainer -p 80:80 ubuntu
					6.connect to bash terminal of running container:
						sudo docker exec -it mycontainer bash
					7. !to kill a container :
						sudo docker kill containerid
					8.restart docker container:
						sudo docker restart containerid
					9. remove docker container:
						sudo docker rm containerid
					10.commit done changes to container:
						sudo docker commit containerid custom-image


			--docker volumes:
					docker volumes are persistant storages, they can be safely attached and removed from containers

			--docker networks:
					a docker network is basically a connection between one or more containers.

			--docker swarm nodes and services

	-docker repository
		Storage location for docker image, these images can be versioned as well.
		# Commands
			1. sudo docker pull ubuntu
			2. sudo docker tag existing-custom-image username/new_name-given-to-this-existing-image
			3. sudo docker login
			4. sudo docker push



	-docker compose
		docker compose can let you launch multiple container at the same time

	-docker swarm
		(swarm or cluster) its a orchestration tool that allows us to manage multiple container


<h2>Docker files
	docker files are basically scripts that you can write and then build into an image the image can be run to create the container. Its like shell script. create a file named DOCKERFILE.</h2>
	# command

		1. sudo docker bulid .

<h2>Docker FORMAT</h2>

	FROM
	ADD
	COPY
	RUN: Use this to run commands that you want to run only during the creation of a container.
	WORKDIR
	CMD: Use this if you want to run commands after container starts<br/>
	VOLUME
	EXPOSE this instruction tells what port the container should be exposed at. But this can only happen for internal network the host will not be able to access the container from this port.
	ENTRYPOINT
	LABEL: Allows to add metadata to your image

</h2>

<h2>Docker file best practices</h2>
	<h6>.dockerignore:</h6>

	decople applications(eg put database in seperate container and application in different container)

<h2>Docker storage</h2>

	-Volumes(uses --volume)
		--commands:
			1.sudo docker volume create give-volumne-name
			2.sudo docker volume ls
			3.sudo docker volume inspect give-volumne-name
			4.sudo docker volume rm give-volumne-name
			5. remove all volumes at once:
				sudo docker volume prune
	-Bind mount(uses --mount)
	-Tmpfs mount(uses --mount)

In situation where you have to write in docker's writable layer you can make use of specific storage drivers.

	These drivers are:
		--overlay
		--aufs
		--devicemapper
		--btrfs
		--vfs

## Docker networking

A docker is basically a connection between one or more containers.

* bridge
		--default docker bridge network
		--custom docker bridge network
		#commands
			1.Create a bridge network
				sudo docker network create --driver bridge assign_new_name_to_network
			2.list all networks
				sudo docker network ls
			3.inspect network
				sudo docker network inspect assign_new_name_to_network
			4.assign a container our created network
				sudo docker run -it -d --network assign_new_name_to_network --name Mycon ubuntu
			5.Inspect container
				sudo docker container inspect Mycon

* overlay
		--docker daemon hosts that are connected by means of overlay network can communicate with each other
		--outside of host, inter docker daemon communication is possible.
		#commands
			1.create overlay network
				sudo docker network create --driver overlay fun-net
			2.assign our created overlay netework named fun-net to a container:
				sudo docker run -it -d --network fun-net --name Myoverlaycon ubuntu

* host
		--docker containers that are connected to hosts
		--the container shares their host ip they dont have there own ip address
			1.assign a host network to a containers
				sudo docker run -it -d --network host --name mycontainer nginx:latest
			2.inspect the container
				sudo docker container inspect mycon
			3.get the nginx page
				curl localhost

* macvlan

* none

## Docker compose
## Orchestration
## Docker swarm

works on worker manager concept, where manager tells push tasks to worker nodes.

		#Commands:
		1. sudo swarm init
			o/p: generates a token
		2. sudo docker swarm join --token string_of_char_as_tokens
		3. sudo docker network create --driver overlay fun-net
		4. sudo docker network ls
		5. sudo docker ps

		--services is an command that allows us to define various parameters in a single service
		#command
		1. sudo docker service create --name fun-service --network fun-net --replicas 3 nginx:latest
		2. sudo docker service ps fun-service
		3. sudo docker service rm fun-service

## ECR & ECS

## Monitoring in Docker

## Kubernetes

#Commands:
	1. Pull:
		docker pull ubuntu
	2. List all images:
		sudo docker images
	3. Run a container into a interactive detached mode with terminal:
		sudo docker run -it -d ubuntu
	4. List all containers:
		sudo docker ps -a
	5. Add name to your container(default:docker will assign random name to your container) with port exposed:
		sudo docker run -it -d --name mycontainer -p 80:80 ubuntu
	6. Connect to bash terminal of running container:
		sudo docker exec -it mycontainer bash
	7. !to kill a container :
		sudo docker kill containerid
	8. Restart docker container:
		sudo docker restart containerid
	9. Remove docker container:
		sudo docker rm containerid
	10.Commit done changes to container:
		sudo docker commit containerid custom-image
	11.Create a new volume named give-volumne-name
		sudo docker volume create give-volumne-name
	12.List all volumes
		sudo docker volume ls
	13.Inspect a volume named give-volumne-name
		sudo docker volume inspect give-volumne-name
	14.Remove a volume named give-volumne-name
		sudo docker volume rm give-volumne-name
	15.Remove all volumes at once:
		sudo docker volume prune
	16.Attach a volume to container
		sudo docker run -it -d --name ConA --mount source=give-volumne-name,target=/apps ubuntu
		sudo docker run -it -d --name ConB --volume volume-name:/apps ubuntu
		sudo docker run -it -d --name ConA --mount source=give-volumne-name,target=/apps,readonly ubuntu
	17.Attach a bind mount to container:
		sudo docker run -it -d --name ConC --mount type=bind,source=/home/Downloads/random_folder,target=/apps ubuntu
		sudo docker run -it -d --name ConC --mount type=bind,source=/home/Downloads/random_folder,target=/apps,readonly ubuntu

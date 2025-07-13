Docker is a system of containers that contain code and the ideal code environment. This means with a docker container any piece of code can be run on any machine.


**Multiple Docker Containers**
Run multiple containers with a docker-compose.yml file. Volumes can be created as shared files across containers. 

docker images
	show all docker images

docker ps
	show all running docker containers

docker run img_name
	--name container_name
	-p port
	-d detached
		make cmd available after run
		make container run in the background
	-v "$(pwd):/directory" 
		mount volume



docker container stop CONTAINER_ID
	stop the container

Mount drive
	docker run --name fastapi-container -p 80:80 -d -v "$(pwd):/code" fastapi-img


IDE
open IDE in container
File
	open folder
		select code and open

run container with gpu on ubuntu 22.04
	sudo docker run --runtime=nvidia -it --rm nvcr.io/nvidia/tensorflow:24.07-tf2-py3-igpu
	you can always use image IDs

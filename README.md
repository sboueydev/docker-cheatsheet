# Personal Docker Cheatsheet
Listed below are some of my most commonly used commands / workflows.

## TOC
- [Workflow](#workflow) 
- [Other Common Commands](#other-common-commands) 
- [Example Dockerfile](#example-dockerfile) 
- [Shortcuts](#shortcuts) 

### Workflow
- Create a dockerfile

- Build image from dockerfile 
	- docker build -t imagename:tag .
	*Note: do not forget the dot*
		
- Run (create and start) container
	- docker run -ti --name containername imagename:tag command 
	- docker run -ti -v "$(pwd)"/absolutepathincontainer/ --name containername imagename:tag command
	- docker run -ti \
          --name containername \
          --mount source=nameofvolume,target=/nameoftargetincontainer \
          imagename:tag
	- Or do the same thing as above with -v
		-  docker run -ti \
                   --name containername \
                   -v nameofvolume:/nameoftargetincontainer \
                   imagename:tag
		   
	*Note: this creates an interactive environment. I usually use either sh or bash as the command in order to acces the container from the command line.You can find the volumes in var/lib/docker/volumes*

- Exit the terminal by either typing exit or pressing CTRL + d
	
- Stop container
	- docker stop containername
	
- Start container
	- docker start containername
	
- Access the container's command line again
	- docker exec -ti containername command
	*Note: using docker exec you are able to have multiple instances of terminal running within your container which is highly useful because it can let you do things like edit a scss file in terminal while watching and compiling it in another. I usually use either sh or bash as the command for this as well.*
	
### Other Common Commands
- View running containers
	- docker ps 
	
- View all containers 
	- docker ps -a
	
- View images
	- docker images
	
- Remove a container
	- docker rm containername

- Remove an image
	- docker rmi imagename
	
- Rename a container
	- docker rename oldcontainername newcontainername
	
### Example Dockerfile

FROM node:alpine

RUN apk update && apk upgrade && apk add nano

RUN npm install -g gulp

WORKDIR /usr/src/app

COPY package.json /usr/src/app/package.json

RUN npm install

COPY . /usr/src/app

*Note: When using an alpine image base you must use apk instead of apt.*

### Shortcuts
I've used [AutoKey](https://github.com/autokey/autokey) to create my own expandable abbreviations for docker. 
*Note: I also created a Docker usergroup when I configured my installation so that Docker wouldn't require the constant use of "sudo".*

- dbuild = docker build -t
- dbuild? = docker build -t imagename:tag
- dru, drun = docker run
- drut, drunt = docker run -ti --name
- drut?, drunt? = docker run -ti --name containername imagename:tag command
- dex = docker exec
- dext = docker exec -ti
- dex?, dext? = docker exec -ti containername command
	

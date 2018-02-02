**Instruction to start docker container aerodata**  
the Dockerfile can be used to create Docker container with all librares for DL analysis of aerial images.  
run of the image will open jupyter notebook server automatically.

PASSWORD FOR JUPYTER NOTEBOOK: passwd

*to build image use (inside folder with Dockerfile):*  
nvidia-docker build -t aerodata .

*to start a container as background process use:*   
nvidia-docker run -d --rm -p port_on_host:8888 --name $(whoami) -v your_folder:folder_in_container -e "UID=$(id -u)" -e "GID=$(id -g)" aerodata  
where:
* nvidia-docker 	: should be used for using GPU.
* -d 		: to start as daemon.
* -p        : use your port on the host
* --name 	: type name of your container, or use $(whoami) to use your account name.
* -v 		: type here folder to mount in container.
* -e 		: use your user ID to solve permission problem, by leaving "UID=$(id -u)" and "GID=$(id -g)" your uid and gid will be set automatically.  
For fast start you have to change -v arguments only.

*to enter into container as root use:*  
nvidia-docker exec -it <container name> /bin/bash

*to install new packages use:*
1) enter to container as root  
2) use apt-get or pip to install package (pip install keras)

IMPORTANT - if you created files by root and want to have permission do following:  
1) start container with mounted folder in daemon mode.  
2) enter container by: nvidia-docker exec -it <container name> /bin/bash  
3) use: chown -R user:user1 <PATH_TO_FOLDER>

RUNNING AiiDa containers

if you are @ darcco then run
	
	docker run -it --name aiidaNew -v /shared:/shared  aiida /sbin/my_init -- bash -l

you can also download prebuilt image from dockerhub
docker run -it --name aiidaNew -v /shared:/shared  skoneka/docker-aiida /sbin/my_init -- bash -l
there is aufs bug which sometimes pops up 
so if you see this error when the container starts
 
 * Starting PostgreSQL 9.3 database server                                                        
 * The PostgreSQL server failed to start. Please check the log output:
  2015-05-14 13:59:29 UTC FATAL:  could not access private key file "/etc/ssl/private/ssl-cert-snakeoil.key": Permission denied
                               

you have to remove the downloaded image `docker images` `docker rmi docker-aiida-image-id`
and build the image on your own
  `git clone https://github.com/BIGDATA2015-AIIDA-EXTENSION/AiiDA-Docker `
  `cd AiiDa-Docker; docker built -t aiida .`


Once you have the docker container running dont `Crtl-D` because it will stop the container, you can reattach to a running container using 

	> docker ps 
		(to find the CID of your container)
	> docker attach <cid>

Once you are inside the container to the following steps:
 
- set 'PermitRootLogin yes' in /etc/ssh/sshd_config; then `service ssh restart`, test ssh root@localhost inside container
- copy dalco ~/.ssh/id_rsa.pub key to container /root/.ssh/authorized_keys
- check container IP address using ifconfig, if you are outside of container you can use `docker inspect <CID> | grep IP` to find it

For conveniance add the container IP address to /etc/hosts at the host machine
Try logging in with `ssh root@containerIP`

the ip address is going to change if you restart you container!

if you restart container then you also need to run `service ssh restart`

remember about commands: `docker ps`, `start`, `stop`, `run`, `inspect`

May Docker be with you!

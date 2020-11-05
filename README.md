# docker

**pull cuda cudnn tensorflow ready to use image:**

docker pull nvcr.io/nvidia/tensorflow:19.02-py3

**create container with cetain GPU and portforwarding to be able to connect to a jupter notebook for exmaple:**

`docker run -it --shm-size=1g --ulimit memlock=-1 --gpus device=1 --name -p 1234:1234 containername imagename`

**restart container to run it permanently:**

`exit`

`docker start containername`

**get into running container**

`docker exec -it containername bash`

**activate venv environment**

`source /home/venvname/bin/activate`

**Run jupyter notebook Inside the Container:**

`jupyter notebook --ip 0.0.0.0 --no-browser --allow-root --port 1234`

**Host machine access this url:**

[localhost:1234](localhost:1234)

**stop container**

docker stop containername

**to start a Training and detach it from console, so one can disconnect without stopping**

`screen` to start screen session.

control + a + d to detach.

`screen -r` to resume

**view running containers**

`docker ps`

**view all containers**

`docker container ls -a`

**refresh bash**

`source ~/.bashrc`

**save image as tar.gz**

`docker save myimage:latest | gzip > myimage_latest.tar.gz`

**load image from tar.gz**

`docker load < myimage_latest.tar.gz`

# git 

## change master to an older commit

```bash
git checkout 307a5cd        # check out the commit that you want to reset to 
git checkout -b fixy        # create a branch named fixy to do the work
git merge -s ours master    # merge master's history without changing any files
git checkout master         # switch back to master
git merge fixy              # and merge in the fixed branch
git push                    # done, no need to force push!
```

## how to make a fork of a public repository private

First, duplicate the repo as others said (details here):

Create a new repo (let's call it private-repo). Then:

```bash
git clone --bare https://github.com/exampleuser/public-repo.git
cd public-repo.git
git push --mirror https://github.com/yourname/private-repo.git
cd ..
rm -rf public-repo.git
```

Clone the private repo so you can work on it.

```bash
git clone https://github.com/yourname/private-repo.git
cd private-repo
make some changes
git commit
git push origin master
```

To pull new hotness from the public repo:

```bash
cd private-repo
git remote add public https://github.com/exampleuser/public-repo.git
git pull public master # Creates a merge commit
git push origin master
```

# docker/linux

**view logfile live**

tail -f logfile.log

**attach to docker-compose logs(contol+c to detach)**

sudo docker-compose logs -f -t --tail=100

**use standard kernel of env for jupyter notebook**

`python3 -m ipykernel install --user`

**look for running processes on GPU**

`nvidia-smi`

**if process is for some reason not listed, list it with:**

`fuser -v /dev/nvidia`

**kill process by ID**

`kill -9 ID`

**end all jupyter notebooks if no permission to shut down regularly**

 https://stackoverflow.com/questions/50917379/cannot-stop-jupyter-notebook, 
 
 Issue not resolved: https://github.com/jupyterhub/jupyterhub/issues/1377

`pkill jupyter` 

**pull cuda cudnn tensorflow ready to use image:**

docker pull nvcr.io/nvidia/tensorflow:19.02-py3

**create container with cetain GPU and portforwarding to be able to connect to a jupyter notebook for exmaple:**

`docker run -it --shm-size=1g --ulimit memlock=-1 --gpus device=1 -p 1234:1234 --name containername imagename`

**restart container to run it permanently:**

`exit`

`docker start containername`

**get into running container**

`docker exec -it containername bash`

**activate venv environment**

`source /home/venvname/bin/activate`

**Run jupyter notebook Inside the Container:**

`jupyter notebook --ip 0.0.0.0 --no-browser --allow-root --port 1234`

**access jupyter notebook via ssh**

`ssh -N -f -L localhost:8888:localhost:8889 remote_user@remote_host`

**Host machine access this url:**

[localhost:1234](localhost:1234)

**stop container**

docker stop containername

**to start a Training and detach it from console, so one can disconnect without stopping**

`screen -ls` to view running sessions and their pids.

`screen` to start screen session.

control + a + d to detach.

control + a + \ to stop.

`screen -r [pid]` to resume a session

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

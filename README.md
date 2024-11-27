# Spark in Docker

This Repository is going to show how you can leverage Spark using a Docker container paired with Jupyter Notebooks for a nice development environment. To start a prerequisite is that you have Docker installed.

On Mac the easiest way to install Docker Desktop is using homebrew.

Run ```brew install docker``` in your terminal and Docker will be ready to go. 

Another way is to install Docker via the installer for [Mac](https://docs.docker.com/desktop/setup/install/mac-install/) or here for [Windows](https://docs.docker.com/desktop/setup/install/windows-install/).

Make sure on Windows that you have enabled under Settings to use the WSL2 based engine and under the Resources Tab that you allow _file sharing_ between Docker and your local file system.

## Getting the Docker container

We are using the container from Jupyter Docker Stacks, they are pushing their images recently to the Quay.io registry. You can also use older images on the Docker Hub, but they aren't updated.

Before getting the Docker Image Registry make sure that you are in a directory where you want to work. As we are using the current directory to save the notebooks and files we are working with, it is necessary to go into the desired working directory (use ```cd path/to/your/workingdirectory```).

Now we can start by pulling the Image from the registry by executing
```bash
docker pull quay.io/jupyter/all-spark-notebook:latest
```

This will downloads the standard image provided by Jupyter.

Now you can finally execute
```bash
docker run -it --rm -p 8888:8888 -v "$(pwd)":/home/jovyan/work quay.io/jupyter/all-spark-notebook:latest
```

The docker container will run and you will see the docker container logs and output. Inside the output in your terminal you can either click on the provided links starting with "http://127.0.0.1:8888/lab?token=XXXXXX" or type in localhost:8888 in your Browser. You will need to copy the token to access the notebooks.

You can also run the container in detached mode with the following command including a password config
```bash
docker run -d --rm -p 8888:8888 -e JUPYTER_TOKEN='your_password' -v "$(pwd)":/home/jovyan/work quay.io/jupyter/all-spark-notebook:latest
```
Again you can access the noteboook by typing in localhost:8888 into your Browser. If you want to see the token use ```docker logs <your container>```.

HINT: For Windows users you may need another command as `$(pwd)` based on Terminal or PowerShell. You could also include the whole path of the directory you might want to use (e.g. C:/your/path/to/workingdirector)

Have fun using Spark on Jupyter!

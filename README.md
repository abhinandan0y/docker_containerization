# Learn_Docker
Follow the steps to create your own docker image and run app platform independent.

#### create Dockerfile
```
# Use an official base image#os
FROM ubuntu:23.04

# Set the working directory
#WORKDIR /usr/src/app
WORKDIR /home/bioinfo2/Downloads/progenesis/Snakemake/snpSnakemake
# Update the package repository and install necessary software
RUN apt-get update && \
    apt-get install -y \
#    software-properties-common \
#    build-essential \
#    curl \
#    wget \
#    git \
#    && rm -rf /var/lib/apt/lists/* \
    snakemake

# Copy all files to the container
COPY . .

# Expose the port your app runs on (if applicable)
# EXPOSE 3000

# Define the command to run your app
CMD ["./test.sh"]
#CMD ["./your_start_script.sh"]
```
#### content inside shell file
```
##test.sh
#!/bin/bash
echo "Strated Docker"
echo "Test Pipeline Running"
snakemake -j -s ./snakemake_test_steps_pipeline.smk
```
#### build the docker with all details in script
```docker build -t test_snakemake . ```

#### to directly run the container
```
docker run -it --name my-container test_snakemake 
```
#### to get inside shell
```
docker run -it --name my-container test_snakemake /bin/bash
# for installing and making any changes required but it will only be inside docker.
ERRORS:
docker exec -it my-container /bin/bash
Error response from daemon: Container cb5e45684296aaf31fd0064972fa63b42abd081cdb1a2803fcd15961a5894421 is not running
Sol:
sudo systemctl restart docker.socket docker.service
docker rm -f <container id>
#your last resort for critical systems, because restarting docker socket and services while you have running containers have some potential complications. Some of them are as follows:

Loss of Logs: You might loose some logs during startup.
Orphaned Processes: In some rare cases, restarting Docker might leave behind orphaned container processes. These can consume resources and might need to be manually killed.
Potential for Data Loss: In very rare cases, there might be potential for data loss, especially if containers were in the middle of write operations when Docker was restarted.
```
#### stop or remove container
```
docker stop my-container
docker rm my-container
```
#### check logs; run from outside docker
```docker logs snpsnakemake```
### How to get your docker image from one system and run on another system?
```
docker export -o testsnakemake.tar my-container
#output = snpsnakemake.tar

Import the Docker Container:
docker import testsnakemake.tar new_image
output: sha256:d5b8fa51895d4a0e16fa2e4a196e2b7bf2950d1a33d4fc7786c1d1bea93c7a80

Run the Container:
docker run -it --name new_container_name_test new_image /bin/bash
#If your container runs a service in the background (daemonized), you might want to use the -d option instead of -it:

docker ps -a
CONTAINER ID   IMAGE            COMMAND        CREATED         STATUS                     PORTS  NAMES
c65d8d2f92f2   new_image_test   "/bin/bash"    5 minutes ago   Exited (0) 2 minutes ago  new_container_name_test

```
#### Get all the files in the docker container
```
The cp command can be used to copy files.

One specific file can be copied TO the container like:

docker cp foo.txt container_id:/foo.txt
One specific file can be copied FROM the container like:

docker cp container_id:/foo.txt foo.txt
For emphasis, container_id is a container ID, not an image ID. (Use docker ps to view listing which includes container_ids.)

Multiple files contained by the folder src can be copied into the target folder using:
#from source to target in docker
docker cp src/. container_id:/target
#from docker to host target
docker cp container_id:/src/. target
```
###Map ports: -p allows you to map ports between the container and the host:

```bash
docker run -p 8080:80 nginx:latest
```
**#Knowlegde is FREE but Solution is Your's🤘🏻**

**Keep on Learning and Executing...🏃🏻** contact@:bioinformaticsfuture@gmail.com
<div style="width: 100%;">
  <img src="https://www.bioinformaticsfuture.com/images/bioinformatics_lab.png" style="width: 100%;" alt="bioinformatics_lab.png">
</div>

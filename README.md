# learn_docker
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
CMD ["./snp.sh"]
#CMD ["./your_start_script.sh"]
```
#### content inside shell file
```
snp.sh
#!/bin/bash
echo "Strated Docker"
echo "SNP Pipeline Running"
snakemake -j -s ./snakemake_snp_steps_pipelineFinal.smk
```
#### build the docker with all details in script
```docker build -t snp_snakemake . ```

#### to directly run the container
```
docker run -it --name my-container snp_snakemake 
```
#to get inside shell
```
docker run -it --name my-container snp_snakemake /bin/bash
#### for installing and making any changes required but it will only be inside docker.
```
#### stop or remove container
```
docker stop my-container
docker rm my-container
```
#### check logs; run from outside docker
```docker logs nanopore_backend```



**#Knowlegde is FREE but Solution is Your's🤘🏻**

**Keep on Learning and Executing...🏃🏻** contact@:bioinformaticsfuture@gmail.com
<div style="width: 100%;">
  <img src="https://www.bioinformaticsfuture.com/images/bioinformatics_lab.png" style="width: 100%;" alt="bioinformatics_lab.png">
</div>

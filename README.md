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
EXPOSE 80

# Define the command to run your app
CMD ["./snp.sh"]
#CMD ["./your_start_script.sh"]
```
**#Knowlegde is FREE but Solution is Your's🤘🏻**

**Keep on Learning and Executing...🏃🏻** contact@:bioinformaticsfuture@gmail.com
<div style="width: 100%;">
  <img src="https://www.bioinformaticsfuture.com/images/bioinformatics_lab.png" style="width: 100%;" alt="bioinformatics_lab.png">
</div>

# Docker File


## Author
 ** Dev Tomar

## command to build Docker image with docker file 

sudo docker build -t centos:ptm .

## -t for taging image 

##command after image build to up docker container  and docker 8080 port is bind up with base machine port 7080
sudo docker run -p 7080:8080 --name pymoncat -i -t centos:ptm 

# docker_ex1
Sep22 course assignment

# install docker
# create dir for the exercise
mkdir docker_ex1
touch Dockerfile
# copy code from repo
# build docker image
docker build .
# run the container
docker -d -p 8080:80 <image_id>
# visit address http://localhost:8080
# add a new html file to the container
docker cp index.html <container_id>:/var/www/html
# check file exists
docker exec -it <container_id> /bin/bash
cd /var/www/html
apt-get update && apt-get install nano
nano index.html
# create dir called app & add another html file
mkdir app
# copy html code from repo
touch index.html
# update the dockerfile to include the contents of app dir (before CMD line)
COPY app /var/www/html
# build a new image and run with volume to nginx
docker run -d -p 80:80 -v $(pwd)/nginx:/usr/share/nginx/html nginx
# create an html file in the host volume
echo "Hello from second file!" > $(pwd)/nginx/second.html

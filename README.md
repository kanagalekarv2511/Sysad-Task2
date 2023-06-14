# Sysad-Task2
============================
Images built Backed on Dockerfiles 

root@vaibhavtest:~# cat Dockerfile.myappwed

FROM ubuntu:latest
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:
RUN mkdir /root/inputfiles
RUN mkdir /root/scripts
COPY ./inputfiles /root/inputfiles
COPY ./scripts /root/scripts
RUN /root/scripts/genStudent.cust
RUN /root/scripts/permit.cust
RUN apt update  && apt-get install -y apache2
RUN mkdir /var/www/html/gamma-z.hm
COPY ./inputfiles/000-default.conf /etc/apache2/sites-available/


root@vaibhavtest:~# cat Dockerfile-db-final

FROM postgres:latest
ENV POSTGRES_PASSWORD=mysecretpassword
COPY ./inputfiles/cleansd.txt /tmp
ADD ./scripts/postgrescreatetable.sql /docker-entrypoint-initdb.d/

And uploaded to Git repository (Packages ) 

======================================================

Assumptions -- > 

SysAdm Task1 is complete , scripts and Input files are on Virtual Machine ( Ubuntu ) 
Please install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
Along with necessary keys 

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
 sudo chmod a+r /etc/apt/keyrings/docker.gpg
Use the following command to set up the repository:


 echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
Note


==============================================================
Pull App and Web ( Apache packages from Github ) 

docker pull ghcr.io/kanagalekarv2511/myappweb:latest

Sample outoput 

root@vaibhavtest:~# docker image ls
REPOSITORY                          TAG       IMAGE ID       CREATED          SIZE
ghcr.io/kanagalekarv2511/myappweb   latest    f863aaae4d18   56 minutes ago   37.2GB



======================================================

Pull DB also 

docker pull ghcr.io/kanagalekarv2511/mydb:latest

root@vaibhavtest:~# docker image ls
REPOSITORY                          TAG       IMAGE ID       CREATED          SIZE
ghcr.io/kanagalekarv2511/myappweb   latest    f863aaae4d18   58 minutes ago   37.2GB
ghcr.io/kanagalekarv2511/mydb       latest    d382bf5bb811   4 hours ago      379MB

=====================================================================================

Docker Compose File 

root@vaibhavtest:~# cat docker-compose-myappwebdb.yaml
version: "2.18.1"
services:
  myappweb:
    image: ghcr.io/kanagalekarv2511/myappweb:latest
    ports:
      - '80:80'

  mydb:
    image: ghcr.io/kanagalekarv2511/mydb:latest
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=mysecretpassword
    ports:
      - '5432:5432'

=================================================
Additional Notes 

root@vaibhavtest:~# echo "# Sysad-Task2" >> README.md

git init

git add README.md

git commit -m "first commit"

git branch -M main

git remote add origin https://github.com/kanagalekarv2511/Sysad-Task2.git

git push -u origin main

git add Dockerfile-db-final

git commit -m "Dockerfile-db-final Added"

git push https://github.com/kanagalekarv2511/Sysad-Task2


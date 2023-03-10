# Docker
 Docker é Legal!


# O que é Docker?
- Docker é uma plataforma Open Source escrito em Go, uma linguagem de programação de alto desempenho desenvolvida dentro do Google, que facilita a criação e administração de ambientes isolados.

## Containers vs VMs

- O Docker possibilita o empacotamento de uma aplicação ou ambiente inteiro dentro de um container

## Instalando o Docker no Ubuntu Server 22.04  (Eu AMO LINUX)

### Linux Ubuntu 22.04
**Pré-requisito:**
* Kernel > 3.8 
* Sistema x64

 ### Atulizanção e Instalação
* $ sudo apt update
* $ sudo apt install docker.io -y

ou

* $ sudo apt install curl -y
* $ sudo curl -fsSL https://get.docker.com/ | sh

__Após a instalação__

* $ docker --version

### Para visualizar os containers ativos, em execução use:

* $ docker ps

Obs.: Para usar o docker sem sudo use o comando abaixo, após isso deslogue e logue novamente 

* $ sudo usermod -aG docker $USER


### Start o primeirio container

* $ docker run hello-world

Obs.: Sempre que uma imagem não estiver no seu HOST Docker irá fazer o download no DockerHub, aluno(a) Cadê sua conta no Dockerhub??

### Listar todos as imagens:
* $ docker images

### Para visualizar todos os containers da sua máquina:
* $ docker ps -a 


### Startando o primeiro container

* $ docker run -ti ubuntu bash
* $ docker run -it debian bash 

Obs.: -ti ou it indica terminal interativo, Ubuntu ou Debian é a imagem a ser utilizada e bash é o comando a ser utilizado; 
Obs2.: Utilizando o -d o container rodar em background; 
Obs3.: Com --name você pode dar um nome ao seu container; 
Obs4.: possível especificar a versão da imagem a ser utilizada:

* $ docker run -ti ubuntu:22.04 bash


Para sair do container e finalizar o processo use Ctrl+D;
Para sair do container sem finalizar o processo use Ctrl+P+Q;
Para voltar para o container ativo pegue o CONTAINER ID usando:


* $ docker ps
### E utilize no lugar do CONTAINER_ID/NAMES o id ou o nome abaixo:


* $ docker attach CONTAINER_ID/NAMES

### Para parar um container em execução sem entrar nele, use:
* $ docker stop CONTAINER_ID

### Para iniciar um container
* $ docker start CONTAINER_ID

### Para pausar um container:
* $ docker pause CONTAINER_ID

### Para despausar um container:
* $ docker unpause CONTAINER_ID

### Para saber quanto seu container esta consumindo:
* $ docker stats CONTAINER_ID

### Para saber como os processos estão consumindo os recursos do seu container:
* $ docker top CONTAINER_ID

### Retorna os processos dentro do container

### Para ver os logs do container:
* $ docker logs CONTAINER_ID

### Para remover um container:
* $ docker rm CONTAINER_ID
* $ docker rm -f CONTAINER_ID

### Remover todos os containers parados
* $ docker container prune

### Use -f para remover forçadamente o containers que estão em execução. 

### Para remover uma imagem:
$ docker rmi IMAGEM_ID
$ docker rmi -f IMAGEM_ID
### … possível utilizar o -f.

### Limitando CPU e MEM dos containers e como usar Docker Update

* $ docker inspect CONTAINER_ID

### Para saber o máximo de memória que seu container pode utilizar (0 indica sem limite):

### $ docker inspect CONTAINER_ID | grep -i mem
### Para limitar a memória a ser utilizada:
* $ docker run -ti --memory 512m --name novo_ubuntu
* ou -m
* $ docker run -ti -m 512m --name novo_ubuntu

### Para limitar a memória do container em execução:
* $ docker update -m 256m CONTAINER_ID 
### Em vez de CONTAINER_ID pode usar o nome
* $ dcoker update -m 256m novo_ubuntu

### Para limitar o uso de CPU do meu container:
* $ docker run -ti --cpu-shares 1024 --name container1 ubuntu
### Para verificar se foi atribuido corretamente:
* $ docker inspect container1 | grep -i cpu

### Para limitar o uso de CPU de um container em execução:

* $ docker update --cpu-shares 512 container1

### Volumes e container data-only

### Volumes são compartilhamentos entre o container e o host
* $ docker run -ti -v /home/ubuntu/volume:/volume ubuntu /bin/bash

### Para criar um container com volume mapeado:
* $ docker run -ti -v /path/to/my/host/volume:/volume ubuntu

### Container data-only possui apenas volumes para compartilhar com outros containers
* $ docker create -v /data --name dbdados ubuntu

## Dockerfile
(https://docs.docker.com/engine/reference/builder/)




### Contruindo um container a partir de um Dockerfile

* $ docker build .


### Para tagear uma imagem:
* $ docker build -t image_name:1.0 .

### Para confirmar:
* $ docker images

### Para criar o container a partir da imagem criada:
* $ docker run -ti image_name:1.0

### Docker login, docker push, docker pull e o dockerhub

### Para ver as camadas do container:
* $ docker history image_name:1.0

### Para renomear uma imagem:
* $ docker tag IMAGE_ID new_name:1.0

### Fazer login no Dockerhub
* $ docker login

### Subir uma imagem local para o seu Dockerhub
* $ docker push new_name:1.0 **mesmo nome do seu usuário criado no Dockerhub**

### Para confirmar e saber quais imagens você possui em seu repositório:
* $ docker search user_name

### Para fazer pull de uma imagem:
* $ docker pull user_name/image_name

### Para utilizar a imagem do pull anterior:
* $ docker run -ti user_name/image_name


* $ docker run -d -p 5000:5000 --restart=always --name new_name image_name
-d para rodar como um daemon; -p linkar a porta do docker host com a do container; --restart caso o container morra, assim que o docker voltar o container sobe; --name dar nome ao container


### Passando um servidor de DNS para responder suas requisições
* $ docker run -ti --dns 8.8.8.8 debian
* $ cat /etc/resolv.conf

### Dar hostname ao docker
* $ docker run -ti --hostname conatiner debian (nome interno ao container)
* $ cat /etc/hostname

### Como linkar um container a outro
* $ docker run -ti --name ping ubuntu
* $ docker run -ti --link container1 --name pong ubuntu

* $ ping pong
* $ cat /etc/resolv.conf
* $ cat /etc/hosts

### Como expor a porta do container
* $ docker run -ti --expose 80 debian

### Linkar IP do host com o IP do container
* $ docker run -ti --publish 8080:80 debian
* $ docker run -ti -p 8080:80 debian





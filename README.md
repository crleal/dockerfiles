Colocar a data da maquina igual a do host:

-v /etc/localtime:/etc/localtime:ro

Programas graficos:

-e DISPLAY=unix$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix


Comando Dockers


- Baixar imagem:      docker pull [nome da imagem] 
- Listar imagens:       docker images
- Iniciar a imagem:    docker run [nome da imagem]
- Listar containers:    docker ps -a
- Log um container:  docker logs <nome_container>  
             (OBS: Para acompanhar em tempo real os logs de um container que esteja rodando, basta adicionar o parâmetro -f.)
- Desligar um container:     docker stop <id do container>
- Reiniciar um container:     docker start <id do container>
- Remover um container:    docker rm -f <nome_container>  
- Remove containers:         docker rm <nome_contauner>
- Remover uma imagem:    docker rmi -f <nome_imagem>  


- Remove todos os containers:   docker rm -f  $(sudo docker ps -aq)
- Remove todas as imagens:      docker rmi $(sudo docker images -aq)


- Executa comandos no container:    
    docker exec [id do container] [comando]
    docker exec -it <id do container> bash 
        ( -i modo interativo, -t alocado um pseudo-TTY, por fim o comando bash 
será executado na “máquina” e lhe dará acesso a  seu shell.)
- Copiar um arquivo do container para o host:
     docker cp <nome_container>:/caminho/no/container /caminho/no/host  
     Exemplo: docker cp app1:/home/ec2-user/log.txt /logs

EXEMPLOS:

**********************************************************************************************
Remover dangling images

# docker rmi $(docker images -q -f dangling=true)  

"Dangling images" são, basicamente, imagens sem uma tag. Se você alguma(s) 
vez(es) rodou um Dockerfile que falhou, provavelmente você deve ter uma 
ou mais imagens sem tags. Para removê-las, basta usar o comando acima.
**********************************************************************************************
# docker pull nginx
# docker run -d -p 80:80 nginx
O parâmetro "-d" informa que a "máquina" será executada em background e 
o parâmetro "-p" informa que toda requisição da porta 80 do hospedeiro X 
será redirecionada para a porta 80 da "máquina" que acabou de ser iniciada. 
***********************************************************************************************
Build de uma imagem
# docker build -t <nome_da_imagem> <caminho_para_dockerfile>  

OBS: Lembre que as imagens são compostas de camadas (layers) e que o 
Docker usa caching para fazer o build somente das camadas que tiveram
alguma mudança. Recentemente, o Docker publicou uma Image Specification, 
que explica como tudo isso funciona. Para buildar uma imagem sem 
utilizar caching, adicione a opção --no-cache ao comando.
**********************************************************************************************
https://github.com/crosbymichael/dockerui

# sudo docker run -d -p 9000:9000 --privileged -v /var/run/docker.sock:/var/run/docker.sock dockerui/dockerui

Open your browser to http://<dockerd host ip>:9000
**********************************************************************************************
Executando um container MongoDB

No DockerHub está disponível a imagem oficial do Mongo, basta executar o comando abaixo para ter o Mongo rodando em um container.

# docker run -d -v $PWD/mongodata:/data/db -p 27017:27017 mongo

A parte do $PWD/mongodata: pode ser substituida pelo caminho de sua preferencia, este é o local onde o Mongo irá salvar os dados.

Se preferir executar no modo efemero (perdendo todos os dados ao reiniciar o container) execute apenas docker run -d -p 27017:27017 mongo
**********************************************************************************************
Monitoramento de containers

# docker stats <nome_container>  

OBS: Para ver as estatísticas de todos os containers rodando no host, use:

# docker stats `docker ps | tail -n+2 | awk '{ print $NF }'`  
**********************************************************************************************
*********************************** Supeorvisord *********************************************
https://hub.docker.com/r/fr3nd/supervisor/

# Create configuration for the service
mkdir -p $HOME/supervisor.d
cat << EOF > $HOME/supervisor.d/collectd.conf
[program:collectd]
command=docker run --privileged -v /proc:/mnt/proc:ro fr3nd/collectd
EOF

# Run supervisord
docker run \
  --detach \
  --name supervisord \
  --volume /var/run/docker.sock:/var/run/docker.sock:rw \
  --volume $HOME/supervisor.d:/etc/supervisor/conf.d:ro \
  --volume /var/log/supervisor:/var/log/supervisor:rw \
  --volume $HOME/Pearson:/Pearson \
  fr3nd/supervisor


# View status of the running services
docker exec \
  supervisord \
  supervisorctl status

docker run \
  --detach \
  --name java-supervisord \
  --volume /var/run/docker.sock:/var/run/docker.sock:rw \
  --volume $HOME/supervisor.d:/etc/supervisor/conf.d:ro \
  --volume /var/log/supervisor:/var/log/supervisor:rw \
  --volume $HOME/Pearson:/Pearson \
maluuba/java-supervisor

************************************ Mysql *************************************************


sudo docker pull mysql


***  Para pegar o IP usar sudo docker inspect <id container>
sudo docker run --name mymysql -e MYSQL_ROOT_PASSWORD=root6Beer -d mysql


*** -p 3306:3306  = localhost:3306
sudo docker run -p 3306:3306 --name mymysql -e MYSQL_ROOT_PASSWORD=root6Beer -d mysql
*******************************************************************************************

*********************************** intellij **********************************************


https://hub.docker.com/r/kurron/docker-intellij/


docker run \
       --rm \
       --name intellij \
       --net "host" \
       --env DISPLAY=unix$DISPLAY \
       --user 1000:1000 \
       --volume /tmp/.X11-unix:/tmp/.X11-unix \
       --volume $HOME:/home/developer \
       kurron/docker-intellij:latest


docker run \
       --name intellij \
       --net "host" \
       --env DISPLAY=unix$DISPLAY \
       --user 1000:1000 \
       --volume /tmp/.X11-unix:/tmp/.X11-unix \
       --volume $HOME:/home/developer \
       kurron/docker-intellij:latest

https://hub.docker.com/r/jamesnetherton/docker-intellij-community/

docker run -it \
       --name intellij_community \
       --net "host" \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  -e DISPLAY=unix$DISPLAY \
    --volume $HOME:/home/developer \
  jamesnetherton/intellij-community


******************************* Pulse e skype ***************************
docker run -d \
	-v /etc/localtime:/etc/localtime:ro \
	--device /dev/snd \
	--name pulseaudio \
	-p 4713:4713 \
	-v /var/run/dbus:/var/run/dbus \
	-v /etc/machine-id:/etc/machine-id \
	jess/pulseaudio

docker run \
    --rm \
    --name skype \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
	-v $HOME/.Skype:/home/skype/.Skype \
	-e DISPLAY=unix$DISPLAY \
	--link pulseaudio:pulseaudio \
	-e PULSE_SERVER=pulseaudio \
	--device /dev/video0 \
	jess/skype
******************************************* Chrome ****************************************
 docker run -it \
	--net host \
	--cpuset-cpus 0 \
	--memory 512mb \
	-v /tmp/.X11-unix:/tmp/.X11-unix \
	-e DISPLAY=unix$DISPLAY \
	-v $HOME/Downloads:/root/Downloads \
	-v $HOME/.config/google-chrome/:/data \
	--device /dev/snd \
	-v /dev/shm:/dev/shm \
	--name chrome \
	jess/chrome

********************************************************************************************





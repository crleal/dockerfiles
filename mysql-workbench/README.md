Gerando imagem:

docker build -t mysql-workbench .

Rodando

docker run -d  \
     --net host \
     -v /tmp/.X11-unix:/tmp/.X11-unix \
     -v $HOME/.mysql-workbench:/root/.mysql/workbench \
     -e DISPLAY=unix$DISPLAY \
    --name mysql-workbench \
     mysql-workbench [COMMAND]



docker run -d --net="host" -e DISPLAY=unix$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix mysql-workbench 

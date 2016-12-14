Gerando imagem:

docker build -t firefox-clean .


https://docs.docker.com/engine/installation/ubuntulinux/#adjust-memory-and-swap-accounting
Resolve o problema de limitar a memoria no docker

Rodando


docker run   -d \
            -v $HOME/Downloads:/home/developer/Downloads:rw \
            -v /tmp/.X11-unix:/tmp/.X11-unix \
            -v /dev/snd:/dev/snd \
            -v /dev/shm:/dev/shm \
            -v $HOME/.Xauthority:/home/developer/.Xauthority \
            -v $HOME/.cache/mozilla/firefox/:/home/developer/.cache/mozilla/firefox/  \
            -v $HOME/.mozilla/firefox/:/home/developer/.mozilla/firefox/  \
            --privileged \
            -e uid=$(id -u) \
            -e gid=$(id -g) \
            -e DISPLAY=unix$DISPLAY \
            --net host \
	        --cpuset-cpus 0 \
	        --memory 1024mb \ 
            --name firefox \
            firefox-clean



docker run   -d \
            -v $HOME/Downloads:/home/developer/Downloads:rw \
            -v /tmp/.X11-unix:/tmp/.X11-unix \
            -v /dev/snd:/dev/snd \
            -v /dev/shm:/dev/shm \
            -e DISPLAY=unix$DISPLAY \
            --net host \
            --cpuset-cpus 0 \
            --memory 1024mb \
            --name firefox-docker \
            firefox-clean

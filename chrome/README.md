Como base https://github.com/chrisdaish/docker-chrome

Gerando imagem:

docker build -t chrome .


https://docs.docker.com/engine/installation/ubuntulinux/#adjust-memory-and-swap-accounting
Resolve o problema de limitar a memoria no docker

Rodando


docker run  -v $HOME/Downloads:/home/google-chrome/Downloads:rw \
            -v /tmp/.X11-unix:/tmp/.X11-unix \
            -v /dev/snd:/dev/snd \
            -v /dev/shm:/dev/shm \
            -v $HOME/.config/google-chrome/:/home/google-chrome/.config/google-chrome/ \
            --privileged \
            -e uid=$(id -u) \
            -e gid=$(id -g) \
            -e DISPLAY=unix$DISPLAY \
            --net host \
	        --cpuset-cpus 0 \
	        --memory 512mb \
            --rm \
            --name google-chrome \
            chrome


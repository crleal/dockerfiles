sudo docker run -d \
            -v $HOME/Downloads:/home/user/Downloads:rw \
            -v /etc/localtime:/etc/localtime:ro \
            -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=unix$DISPLAY \
            --name franz sayden/franz


Gerando imagem:

docker build -t skype .

Rodando

docker run -v /tmp/.X11-unix:/tmp/.X11-unix \
	-v $HOME/.Skype:/home/skype/.Skype \
    -v /etc/localtime:/etc/localtime:ro \
	-e DISPLAY=unix$DISPLAY \
	-v /run/user/$UID/pulse/native:/tmp/pulse \
	--device /dev/video0 \
	skype



docker run -d  --name=skype -v /tmp/.X11-unix:/tmp/.X11-unix -v $HOME/.Skype:/home/skype/.Skype -v /etc/localtime:/etc/localtime:ro -e DISPLAY=unix$DISPLAY -v /run/user/$UID/pulse/native:/tmp/pulse --device /dev/video0 skype


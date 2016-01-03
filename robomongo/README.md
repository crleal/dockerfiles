Gerando imagem:

docker build -t robomongo .

docker run -d --net="host" --name=robomongo -e DISPLAY=unix$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix robomongo 




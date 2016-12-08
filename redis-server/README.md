Gerando imagem:

docker build -t redis-server .


https://docs.docker.com/engine/installation/ubuntulinux/#adjust-memory-and-swap-accounting
Resolve o problema de limitar a memoria no docker

Rodando


docker run -d -p 6379:6379 --name redis redis-server




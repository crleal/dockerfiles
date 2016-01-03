Executando um container MongoDB

No DockerHub está disponível a imagem oficial do Mongo, basta executar o comando abaixo para ter o Mongo rodando em um container.

# docker run -d -v $PWD/mongodata:/data/db -p 27017:27017 --name=mongo mongo

A parte do $HOME/mongodata: pode ser substituida pelo caminho de sua preferencia, este é o local onde o Mongo irá salvar os dados.

Os dados no container
docker run -d -p 27017:27017 --name=mongo mongo

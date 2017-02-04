https://hub.docker.com/r/andreptb/maven/
sudo docker run --rm --name maven andreptb/maven:3.3.9-jdk8-alpine  mvn -version

https://hub.docker.com/r/frekele/maven/
sudo docker run --rm --name maven frekele/maven


docker build -t java-jdk8 .

sudo docker run -it --rm --name maven -v "$PWD":/data -v "$HOME"/.m2:/root/.m2 java-jdk8 mvn clean install -Pall -DskipTests 






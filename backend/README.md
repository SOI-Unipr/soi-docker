## build the apache image
docker build -t node .

## run the image - app can be reached out using http://localhost:8080/
docker run --name todo-server -dit -p 8000:8000 node 

## create the newtork
docker network create todo-app-network
docker network create todo-app-network --subnet=10.88.0.0/16

## inspect the network bridge
docker network inspect todo-app-network

## run the image using network and ip
docker run --name todo-server -dit -p 8000:8000 --network todo-app-network --ip 10.88.0.11 node 

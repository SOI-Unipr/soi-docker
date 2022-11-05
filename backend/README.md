## update the Google OAuth credentials and Consent Screen (see lab slides) 
## create a .env file with this values
```
OIDC_CLIENT_ID="xxxxx.apps.googleusercontent.com"
OIDC_SECRET="GOCSPX-xxxxxxx"
OIDC_REDIRECT="http://soi-labdocker.unipr.it:8080"
```

## build the apache image
```
docker build -t node:alpha .
```

## run the image. Server can be reached out using http://localhost:8000 (e.g. trying wget http://localhost:8000/tasks)
```
docker run --name todo-server -dit -p 8000:8000 node:alpha
```

## create the newtork
```
docker network create todo-app-network --subnet=10.88.0.0/16
```

## run the image using network and ip
```
docker run --name todo-server -dit -p 8000:8000 --network todo-app-network --ip 10.88.0.11 node 
```

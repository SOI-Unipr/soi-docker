## update the Google OAuth credentials and Consent Screen (see lab slides) 
## create a .env file with this values
```
OIDC_CLIENT_ID="xxxxx.apps.googleusercontent.com"
OIDC_SECRET="GOCSPX-xxxxxxx"
OIDC_REDIRECT="http://soi-labdocker.unipr.it:8080"
```
Here a valid example
```
OIDC_CLIENT_ID="219491940200-f9faq1l3khpailo5jd7sb9f58s16b6r0.apps.googleusercontent.com"
OIDC_SECRET="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"
```
## build the apache image
```
docker build -t node .
```

## run the image - app can be reached out using http://localhost:8080/
```
docker run --name todo-server -dit -p 8000:8000 node /bin/ash 
```

## create the newtork
```
docker network create todo-app-network --subnet=10.88.0.0/16
```

## run the image using network and ip
```
docker run --name todo-server -dit -p 8000:8000 --network todo-app-network --ip 10.88.0.11 node 
```

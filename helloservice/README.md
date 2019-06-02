# helloservice

## test application
```
cd app
node index.js
```
localhost:8080

## Deploy Cloud Run
Set GCP project
```
gcloud set project [YOUR GCP PROJECT]
```

Build Docker image and upload to Cloud Registry
```
make build
```
or 
```
gcloud builds submit --tag gcr.io/[PROJECT-ID]/helloworld
```

Deploy to Cloud Run
```
make deploy-cloudrun
```
or 
```
gcloud beta run deploy --image gcr.io/[PROJECT-ID]/helloworld
```





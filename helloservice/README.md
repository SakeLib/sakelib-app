# helloservice

## test application
```
cd app
node index.js
```
localhost:8080

## Deploy to Cloud Run
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

## Deploy to AppEngine
```
make gae-standard-deploy
```

## Is there performance defferentiations between Cloud Run and GAE? 
The answer is NO. 
```
ab -n 10000 -c 100 [URL]
```
GAE results 
```
Server Software:        Google
Server Hostname:        fukudak-playground.appspot.com
Server Port:            443
SSL/TLS Protocol:       TLSv1.2,ECDHE-RSA-CHACHA20-POLY1305,2048,256
TLS Server Name:        fukudak-playground.appspot.com

Document Path:          /
Document Length:        12 bytes

Concurrency Level:      100
Time taken for tests:   41.807 seconds
Complete requests:      10000
Failed requests:        0
Total transferred:      20029763 bytes
HTML transferred:       120000 bytes
Requests per second:    239.19 [#/sec] (mean)
Time per request:       418.071 [ms] (mean)
Time per request:       4.181 [ms] (mean, across all concurrent requests)
Transfer rate:          467.87 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:       45  181  98.1    167     747
Processing:   145  231 136.0    202    3259
Waiting:      144  225 134.1    198    3257
Total:        198  413 176.8    367    3412

Percentage of the requests served within a certain time (ms)
  50%    367
  66%    381
  75%    398
  80%    415
  90%    568
  95%    775
  98%    898
  99%    977
 100%   3412 (longest request)
 ```

 Cloud Run results 
 ```
  Server Software:        Google
Server Hostname:        fukudak-playground.appspot.com
Server Port:            443
SSL/TLS Protocol:       TLSv1.2,ECDHE-RSA-CHACHA20-POLY1305,2048,256
TLS Server Name:        fukudak-playground.appspot.com

Document Path:          /
Document Length:        12 bytes

Concurrency Level:      100
Time taken for tests:   39.796 seconds
Complete requests:      10000
Failed requests:        0
Total transferred:      19946305 bytes
HTML transferred:       120000 bytes
Requests per second:    251.28 [#/sec] (mean)
Time per request:       397.957 [ms] (mean)
Time per request:       3.980 [ms] (mean, across all concurrent requests)
Transfer rate:          489.47 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:       48  175  78.6    167     610
Processing:   145  216  60.9    199    1057
Waiting:      144  209  57.8    194    1052
Total:        198  390 111.0    362    1210

Percentage of the requests served within a certain time (ms)
  50%    362
  66%    377
  75%    391
  80%    405
  90%    521
  95%    658
  98%    770
  99%    811
 100%   1210 (longest request)

```

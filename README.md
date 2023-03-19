# Context
If you want to use a blue-green deployment strategy over an endpoint in WSO2 MicroIntegrator Endpoints you need to do a lot of configuration in your endpoint.

Using the Ambassor Pattern you do not need to put that logic into your service, you delegate it to a sidecontainer. An NGINX in this example.

There are some cons also:
* The pod now includes another container. More resources and more complexity during deployments
* You need to think about how to provision that Ambassor configuration
* Observability over that new container, is it may be another point of failure in your chain.

# Examples

## blue

```bash
curl -kis -H "color:blue" http://localhost:8290/backend
HTTP/1.1 200 OK
activityid: bc8e31be-5402-46c4-bbb8-6c09dbebb8e9
Server: nginx/1.23.4
Access-Control-Allow-Methods: GET
X-App-Name: http-echo
X-App-Version: 0.2.3
Access-Control-Allow-Headers:
Content-Type: text/plain; charset=utf-8
Date: Sat, 13 May 2023 12:12:04 GMT
Transfer-Encoding: chunked

"blue backend"
```


## green

```bash
curl -kis -H "color:green" http://localhost:8290/backend
HTTP/1.1 200 OK
activityid: bc8e31be-5402-46c4-bbb8-6c09dbebb8e9
Server: nginx/1.23.4
Access-Control-Allow-Methods: GET
X-App-Name: http-echo
X-App-Version: 0.2.3
Access-Control-Allow-Headers:
Content-Type: text/plain; charset=utf-8
Date: Sat, 13 May 2023 12:12:04 GMT
Transfer-Encoding: chunked

"green backend"
```

## default

```bash
curl -kis http://localhost:8290/backend
HTTP/1.1 200 OK
activityid: bc8e31be-5402-46c4-bbb8-6c09dbebb8e9
Server: nginx/1.23.4
Access-Control-Allow-Methods: GET
X-App-Name: http-echo
X-App-Version: 0.2.3
Access-Control-Allow-Headers:
Content-Type: text/plain; charset=utf-8
Date: Sat, 13 May 2023 12:12:04 GMT
Transfer-Encoding: chunked

"blue backend"
```

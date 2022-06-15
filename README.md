# Task

* Configure nginx that will cache only images, that were requested at least twice
* Add ability to drop nginx cache by request. You should drop cache for specific file only ( not all cache )

# Test
First call
```shell
> curl -X GET -I http://127.0.0.5/i.png
HTTP/1.1 200 OK
Server: nginx/1.21.6
Date: Wed, 15 Jun 2022 22:53:16 GMT
Content-Type: image/png
Content-Length: 196917
Connection: keep-alive
Last-Modified: Wed, 15 Jun 2022 20:17:33 GMT
ETag: "62aa3e5d-30135"
X-Proxy-Status: MISS
Accept-Ranges: bytes
```
Second call
```shell
> curl -X GET -I http://127.0.0.5/i.png
HTTP/1.1 200 OK
Server: nginx/1.21.6
Date: Wed, 15 Jun 2022 22:53:16 GMT
Content-Type: image/png
Content-Length: 196917
Connection: keep-alive
Last-Modified: Wed, 15 Jun 2022 20:17:33 GMT
ETag: "62aa3e5d-30135"
X-Proxy-Status: MISS
Accept-Ranges: bytes
```
Third call
```shell
> curl -X GET -I http://127.0.0.5/i.png
HTTP/1.1 200 OK
Server: nginx/1.21.6
Date: Wed, 15 Jun 2022 22:53:20 GMT
Content-Type: image/png
Content-Length: 196917
Connection: keep-alive
Last-Modified: Wed, 15 Jun 2022 20:17:33 GMT
ETag: "62aa3e5d-30135"
X-Proxy-Status: HIT
Accept-Ranges: bytes
```
Bypass call
```shell
> curl -X GET -I http://127.0.0.5/i.png\?nocache\=true
HTTP/1.1 200 OK
Server: nginx/1.21.6
Date: Wed, 15 Jun 2022 22:53:53 GMT
Content-Type: image/png
Content-Length: 196917
Connection: keep-alive
Last-Modified: Wed, 15 Jun 2022 20:17:33 GMT
ETag: "62aa3e5d-30135"
X-Proxy-Status: BYPASS
Accept-Ranges: bytes
```

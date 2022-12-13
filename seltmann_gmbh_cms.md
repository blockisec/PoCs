# Seltmann GmbH / Content Management System 6 - SQL-Injection


**CVE-ID:** -


**Vendor:** Seltmann GmbH (https://www.seltmann-webdesign.de/)

**Affected Product:** Content Management System

**Affected Versions:** 6

**Vulnerability:** SQL-Injection

**Status:** Unfixed

**Severity:** Critical



## Details

The `id` parameter of the `/index.php` endpoint in the Content Management System of the *Seltmann GmbH* is vulnerable to SQL-Injection.

```http
GET /index.php?controller=index&function=change_lang_redirect&id=1%22&url=something HTTP/2
Host: localhost
[...]
```


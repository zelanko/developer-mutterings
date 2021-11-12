# Test the TLS Versions a Website uses for HTTPS

Yesterday I needed to test the tls versions enabled on an internal website on our company network. I could not use the handy online tools because this site is not on the public internet.
[This jumpnowtek article](https://jumpnowtek.com/security/Using-nmap-to-check-certs-and-supported-algos.html) clued me in to using nmap with a special nmap script. 
I didn't realize that [nmap](https://jumpnowtek.com/security/Using-nmap-to-check-certs-and-supported-algos.html)](nmap.org) is available as a windows utility.

With nmap for windows installed I:

  1. Downloaded nmap script [ssl-enum-ciphers](https://nmap.org/nsedoc/scripts/ssl-enum-ciphers.html).
  2. Ran this from powershell. ```nmap --script $env:USERPROFILE\Downloads\ssl-enum-ciphers.nse -p 443 thesiteineededtotest.mycompany.com```

The result showed the enabled SSL/TLS versions and cyphers.

<pre>Starting Nmap 7.92 ( https://nmap.org ) at 2021-11-11 12:26 Eastern Standard Time
Nmap scan report for thesiteineededtotest.mycompany.com (10.12.13.15)
Host is up (0.077s latency).

PORT    STATE SERVICE
443/tcp open  https
| ssl-enum-ciphers:
|   TLSv1.2:
|     ciphers:
|       TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384 (secp256r1) - A
|       TLS_RSA_WITH_AES_128_GCM_SHA256 (rsa 2048) - A
|       TLS_RSA_WITH_AES_128_CBC_SHA (rsa 2048) - A
|       TLS_RSA_WITH_AES_128_CBC_SHA256 (rsa 2048) - A
|       TLS_RSA_WITH_AES_256_GCM_SHA384 (rsa 2048) - A
|       TLS_RSA_WITH_AES_256_CBC_SHA (rsa 2048) - A
|       TLS_RSA_WITH_AES_256_CBC_SHA256 (rsa 2048) - A
|       TLS_RSA_WITH_CAMELLIA_128_CBC_SHA (rsa 2048) - A
|       TLS_RSA_WITH_CAMELLIA_256_CBC_SHA (rsa 2048) - A
|       TLS_DHE_RSA_WITH_AES_128_GCM_SHA256 (dh 1024) - A
|       TLS_DHE_RSA_WITH_AES_128_CBC_SHA (dh 1024) - A
|       TLS_DHE_RSA_WITH_AES_128_CBC_SHA256 (dh 1024) - A
|       TLS_DHE_RSA_WITH_AES_256_GCM_SHA384 (dh 1024) - A
|       TLS_DHE_RSA_WITH_AES_256_CBC_SHA (dh 1024) - A
|       TLS_DHE_RSA_WITH_AES_256_CBC_SHA256 (dh 1024) - A
|       TLS_DHE_RSA_WITH_CAMELLIA_128_CBC_SHA (dh 1024) - A
|       TLS_DHE_RSA_WITH_CAMELLIA_256_CBC_SHA (dh 1024) - A
|     compressors:
|       NULL
|     cipher preference: server
|     warnings:
|       Key exchange (dh 1024) of lower strength than certificate key
|_  least strength: A

Nmap done: 1 IP address (1 host up) scanned in 10.65 seconds</pre>

I was looking to see that only TLS v1.2 was enabled. And we see that it was.

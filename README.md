```
 _____ _     ____        _        _
|_   _| |   / ___|      | |_ _ __(_)___
  | | | |   \___ \ _____| __| '__| / __|
  | | | |___ ___) |_____| |_| |  | \__ \
  |_| |_____|____/       \__|_|  |_|___/

```

crypto/tls, now with 100% more 1.3.

DO NOT USE THIS FOR THE SAKE OF EVERYTHING THAT'S GOOD AND JUST.

[![Build Status](https://travis-ci.org/cloudflare/tls-tris.svg?branch=master)](https://travis-ci.org/cloudflare/tls-tris)

## Running the NSS test client

```
go run generate_cert.go -ecdsa-curve P256 -host 192.168.64.1 -duration 87600h
go run _dev/server.go 192.168.64.1:4433
```

```
docker build -t tstclnt _dev/tstclnt
docker run -it tstclnt -D -V tls1.3:tls1.3 -o -O -h 192.168.64.1 -p 4433
```
[![Test with Docker Compose](https://github.com/kaiwanyawit-chawankul/ngnix-mountebank/actions/workflows/test.yml/badge.svg)](https://github.com/kaiwanyawit-chawankul/ngnix-mountebank/actions/workflows/test.yml)

# Idea
To run mountebank behind nginx with only one port

```
    location ~ ^/mock(\d+)(.*) {
        set $pass_url http://mountebank:$1;
        rewrite ^/mock(\d+)(.*) $2 break;
        proxy_pass $pass_url;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
```

# Usage

```
make_request http://localhost:8001/setup/imposters
make_request http://localhost:8001/mock4545/api/v1/users/1
make_request http://localhost:8001/mock4546/v2/users/2
```

By this location setup, we don’t need to worry about updating the container again to support more opening ports for mocking service.

# To test locally
open terminal(1)
docker-compose up --build

open another terminal(2)
./test.sh

https://stackoverflow.com/a/22259088

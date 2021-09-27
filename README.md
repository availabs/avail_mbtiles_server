# AVAIL MBTiles Server

[TileServer GL](https://tileserver.readthedocs.io/en/latest/index.html) server
for AVAIL's vector tiles.

## Starting the server

```bash
./start
```

or

```bash
forever start ./node_modules/.bin/tileserver-gl-light --port 9779 --verbose
```

## NGINX sub-route

In NGINX config:

```sh
  location /tiles/ {
    rewrite /tiles/(.*) /$1  break;
    proxy_pass http://127.0.0.1:8080;
    proxy_redirect     off;
    proxy_set_header   Host $host;
  }
```

In TileServer config:

```sh
{
  "options": {
    "paths": {
      "root": ""
    },
    "domains": [ "127.0.0.1:8080" ],
```

```sh
$ cat start
#!/bin/bash

./node_modules/.bin/tileserver-gl-light --verbose --public_url https://foo.bar.org/tiles/
```

See

- [docs](https://tileserver.readthedocs.io/en/latest/usage.html?highlight=public_url#getting-started)
- [maptiler/tileserver-gl/pull/230](https://github.com/maptiler/tileserver-gl/pull/230)

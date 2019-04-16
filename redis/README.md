
The Envoy proxy [configuration](./envoy.yaml) has a redis filter to route egress requests to redis server.


# Usage
1. `docker-compose pull`
2. `docker-compose up --build`
3. Issue redis commands using your favourite redis client such as `redis-cli`
4. Enter the redis container with `docker-compose exec redis /bin/bash`
5. Enter the envoy container with `docker-compose exec proxy /bin/bash`
6. Monitor request success: http://localhost:8001/stats?usedonly&filter=redis.egress_redis.command


## Sample Output:

Use `redis-cli` to issue redis commands and verify they are routed via Envoy:

```
> redis-cli -h localhost -p 1999 set foo foo
OK
> redis-cli -h localhost -p 1999 set bar bar
OK
> redis-cli -h localhost -p 1999 get foo
"foo"
> redis-cli -h localhost -p 1999 get bar
"bar"
```

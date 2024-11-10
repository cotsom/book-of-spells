# Redis

| Command  | Description                                                                         | Usage                                         |
| -------- | ----------------------------------------------------------------------------------- | --------------------------------------------- |
| SET      | Sets the value of a key                                                             | `SET key value`                               |
| GET      | Gets the value of a key                                                             | `GET key`                                     |
| DEL      | Deletes one or more keys                                                            | `DEL key1 [key2 ...]`                         |
| KEYS     | Lists all keys matching a pattern                                                   | `KEYS pattern`                                |
| EXPIRE   | Sets an expiration time on a key                                                    | `EXPIRE key seconds`                          |
| TTL      | Gets the remaining time to live of a key                                            | `TTL key`                                     |
| INCR     | Increments the value of a key                                                       | `INCR key`                                    |
| DECR     | Decrements the value of a key                                                       | `DECR key`                                    |
| LPUSH    | Prepends one or multiple values to a list                                           | `LPUSH key value [value ...]`                 |
| RPUSH    | Appends one or multiple values to a list                                            | `RPUSH key value [value ...]`                 |
| LPOP     | Removes and gets the first element in a list                                        | `LPOP key`                                    |
| RPOP     | Removes and gets the last element in a list                                         | `RPOP key`                                    |
| SADD     | Adds one or more members to a set                                                   | `SADD key member [member ...]`                |
| SMEMBERS | Gets all members in a set                                                           | `SMEMBERS key`                                |
| ZADD     | Adds one or more members to a sorted set                                            | `ZADD key score member [score member ...]`    |
| ZRANGE   | Returns a range of members in a sorted set                                          | `ZRANGE key start stop [WITHSCORES]`          |
| HSET     | Sets field in the hash stored at key                                                | `HSET key field value [field value ...]`      |
| HGET     | Gets the value of a field in a hash stored at key                                   | `HGET key field`                              |
| HDEL     | Deletes one or more fields from a hash stored at key                                | `HDEL key field [field ...]`                  |
| HMSET    | Sets multiple fields in a hash stored at key (Use `HSET` for Redis 4.0.0 and above) | `HMSET key field1 value1 [field2 value2 ...]` |

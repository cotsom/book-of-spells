# Cobalt Strike

### Setting up

**TS:**&#x20;

```bash
sudo ./teamserver ip password ./STF_fsin.profile
```

**Client:**&#x20;

```bash
java -XX:ParallelGCThreads=4 -XX:+AggressiveHeap -XX:+UseParallelGC -javaagent:uHook.jar -jar cobaltstrike-client.jar $*
```



**Start:**

```bash
_JAVA_OPTIONS='-Dawt.useSystemAAFontSettings=on' ./cobaltstrike
```

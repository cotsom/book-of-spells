---
description: Obfuscate Go Tooling
---

# Golang

### garble <a href="#garble" id="garble"></a>

```bash
$ go install mvdan.cc/garble@latest
$ env CGO_ENABLE=1 GOOS=windows GOARCH=amd64 garble -literals -tiny build -ldflags "-s -w -H windowsgui" -trimpath
```

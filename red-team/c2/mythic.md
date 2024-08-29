# Mythic

### Set up

```bash
$ git clone https://github.com/its-a-feature/Mythic

$ cd Mythic

$ sudo make

$ sudo ./mythic-cli start

```

### Get admin pass

```bash
$ sudo ./mythic-cli config get MYTHIC_ADMIN_PASSWORD
```

The default username is `mythic_admin`

### Install agent

```bash
$ sudo ./mythic-cli install github https://github.com/MythicAgents/Athena
```

### installing C2 Profiles

```bash
$ sudo ./mythic-cli install github https://github.com/MythicC2Profiles/http
```

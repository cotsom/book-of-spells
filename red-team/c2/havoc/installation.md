# Installation

### Set up

```bash
git clone https://github.com/HavocFramework/Havoc.git
```



### Dependencies

_After following the steps above we need to install the needed dependecies for the teamserver and compile it to our final executable. Be aware that the teamserver requieres golang 1.18 to be able to compile and run._

**Ubuntu 20.04 / 22.04**

> You must enable Python 3.10 in your APT repositories before you can run the Client successfully.

```bash
sudo add-apt-repository ppa:deadsnakes/ppasudo apt updatesudo apt install python3.10 python3.10-dev
```

**Kali and other Debian based Distros only.**

> The immediate following is for Debian based Distros only.

```bash
sudo apt install -y git build-essential apt-utils cmake libfontconfig1 libglu1-mesa-dev libgtest-dev libspdlog-dev libboost-all-dev libncurses5-dev libgdbm-dev libssl-dev libreadline-dev libffi-dev libsqlite3-dev libbz2-dev mesa-common-dev qtbase5-dev qtchooser qt5-qmake qtbase5-dev-tools libqt5websockets5 libqt5websockets5-dev qtdeclarative5-dev golang-go qtbase5-dev libqt5websockets5-dev python3-dev libboost-all-dev mingw-w64 nasm
```

**Debian 10/11**

> You must setup the `bookworm` repo for Python 3.10.

```bash
echo 'deb http://ftp.de.debian.org/debian bookworm main' >> /etc/apt/sources.listsudo apt updatesudo apt install python3-dev python3.10-dev libpython3.10 libpython3.10-dev python3.10
```

### Building the Teamserver <a href="#id-487f7b22f6" id="id-487f7b22f6"></a>

Install additional Go dependencies:

```bash
cd teamserver
go mod download golang.org/x/sys
go mod download github.com/ugorji/go
cd ..
```

Build and Run:

```bash
# Install musl Compiler & Build Binary (From Havoc Root Directory)
make ts-build

# Run the teamserver
sudo ./havoc server --profile ./profiles/havoc.yaotl -v --debug
```

### Building the Client <a href="#id-487f7b22f6" id="id-487f7b22f6"></a>

```bash
# Build the client Binary (From Havoc Root Directory)
make client-build

# Run the client
./havoc client
```

### Login to Havoc <a href="#login-to-havoc" id="login-to-havoc"></a>

Teamserver information is in profiles/havoc.yaotl

To authenticate:

```bash
Name: Slingshot
Host: localhost
Port: 40056
Username: Neo
Password: password1234
```

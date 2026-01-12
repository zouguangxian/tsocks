# tsocks
**a transparent SOCKS proxying library**

This project is originally hosted by sourceforge http://tsocks.sourceforge.net

Porting to macOS by Zou Guangxian <zouguangxian@163.com> based on http://marc-abramowitz.com/archives/2006/01/29/building-tsocks-on-mac-os-x, with fixes by Mikhail Zakharov <zmey20000@yahoo.com>

## Install
```sh
$ git clone https://github.com/mezantrop/tsocks.git
$ cd tsocks
$ autoconf -f
$ mkdir -p build && cd build
```

### System‑wide installation (requires sudo)

Configure with system paths:

```sh
$ ../configure --prefix=/usr/local --libdir=/usr/local/lib --with-conf=/usr/local/etc/tsocks.conf --enable-debug
$ make
$ sudo make install
```

### User‑local installation (no root required)

If you don’t have permission to install system‑wide, install into a directory under your home:

```sh
$ ../configure --prefix=$HOME/local --libdir=$HOME/local/lib --with-conf=$HOME/local/etc/tsocks.conf --enable-debug
$ make
$ make install
```

This installs everything under `$HOME/local` instead of `/usr/local`.

## Usage
```sh
$ grep '^[^#]' /usr/local/etc/tsocks.conf 
local = 192.168.0.0/255.255.0.0
local = 172.16.0.0/255.240.0.0
local = 10.0.0.0/255.0.0.0
server = 127.0.0.1
server_type = 5
server_port = 8135

$ TSOCKS_DEBUG=2 tsocks git pull
```
or
```sh
$ source /usr/local/bin/tsocks on 
$ telnet example.org
```
or
```sh
$ . /usr/local/bin/tsocks on 
$ telnet example.org
```

## Notes for macOS

* Install OpenSSH from sources (or use Homebrew https://brew.sh port) as the default ssh will not work with the preloaded library:
```sh
brew install openssh
```

*  To permanently sockify all connections using preloaded library, set essential environmental variables on login:
```sh
launchctl setenv DYLD_FORCE_FLAT_NAMESPACE 1
launchctl setenv DYLD_INSERT_LIBRARIES /usr/local/lib/libtsocks.dylib
```

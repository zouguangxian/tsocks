# tsocks
**a transparent SOCKS proxying library**

This project is originally hosted by sourceforge http://tsocks.sourceforge.net

Porting to macOS by Zou Guangxian <zouguangxian@163.com> based on http://marc-abramowitz.com/archives/2006/01/29/building-tsocks-on-mac-os-x, with fixes by Mikhail Zakharov <zmey20000@yahoo.com>

## Install
```
    $ git clone https://github.com/mezantrop/tsocks.git
    $ cd tsocks
    $ autoconf -f
    $ ./configure --prefix=/usr/local --libdir=/usr/local/lib --with-conf=/usr/local/etc/tsocks.conf --enable-debug
    $ make
    $ make install
```
## Usage
```
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
```
    $ source /usr/local/bin/tsocks on 
    $ telnet example.org
```
or
```
    $ . /usr/local/bin/tsocks on 
    $ telnet example.org
```

## Notes for macOS
### If SSH client does not work
Preloaded libraries do not work, when a user, that starts a program is not the same as the owner of the executable. Luckily, there is a number or ways to handle this issue. For example, use sudo:

$ sudo DYLD_FORCE_FLAT_NAMESPACE=1 DYLD_INSERT_LIBRARIES=/usr/local/lib/libtsocks.dylib ssh username@xx.xx.xx.xx
Or, from the technical point of view, nothing can prevent you, from installing ssh client using Homebrew https://brew.sh port:

```
    brew install openssh
```
or building it manually from sources - your user will own ssh binaries.

### To permanently "socksify" all connections using preloaded library
Set essential environmental variables on login:
```
    launchctl setenv DYLD_FORCE_FLAT_NAMESPACE 1
    launchctl setenv DYLD_INSERT_LIBRARIES /usr/local/lib/libtsocks.dylib
```
Or, if the method above doesn't help, add them to your ~/.bash_profile:
```
    export DYLD_FORCE_FLAT_NAMESPACE=1
    export DYLD_INSERT_LIBRARIES=/usr/local/lib/libtsocks.dylib
```

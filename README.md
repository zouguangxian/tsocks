# tsocks
**a transparent SOCKS proxying library**

This project is originally hosted by sourceforge http://tsocks.sourceforge.net

Porting to macOS by Zou Guangxian <zouguangxian@163.com> based on http://marc-abramowitz.com/archives/2006/01/29/building-tsocks-on-mac-os-x, with minor fixes by Mikhail Zakharov <zmey20000@yahoo.com> for macOS.

## Install
    $ git clone https://github.com/mezantrop/tsocks.git
    $ autoconf -f
    $ ./configure --prefix=/usr/local --libdir=/usr/local --with-conf=/usr/local/etc/tsocks.conf --enable-debug
    $ make
    $ make install

## Usage
    $ grep '^[^#]' /usr/local/etc/tsocks.conf 
    local = 192.168.0.0/255.255.0.0
    local = 172.16.0.0/255.240.0.0
    local = 10.0.0.0/255.0.0.0
    server = 127.0.0.1
    server_type = 5
    server_port = 8135

    $ TSOCKS_DEBUG=2 tsocks git pull


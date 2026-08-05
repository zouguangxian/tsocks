# tsocks
**una biblioteca de proxy SOCKS transparente**

Este proyecto está originalmente alojado en sourceforge http://tsocks.sourceforge.net

Portado a macOS por Zou Guangxian <zouguangxian@163.com> basado en http://marc-abramowitz.com/archives/2006/01/29/building-tsocks-on-mac-os-x, con correcciones de Mikhail Zakharov <zmey20000@yahoo.com>

## Instalación
```sh
$ git clone https://github.com/mezantrop/tsocks.git
$ cd tsocks
$ autoconf -f
$ mkdir -p build && cd build
```

### Instalación a nivel del sistema (requiere sudo)

Configurar con rutas del sistema:

```sh
$ ../configure --prefix=/usr/local --libdir=/usr/local/lib --with-conf=/usr/local/etc/tsocks.conf --enable-debug
$ make
$ sudo make install
```

### Instalación local para el usuario (no se requiere root)

Si no tienes permiso para instalar a nivel del sistema, instala en un directorio bajo tu home:

```sh
$ ../configure --prefix=$HOME/local --libdir=$HOME/local/lib --with-conf=$HOME/local/etc/tsocks.conf --enable-debug
$ make
$ make install
```

Esto instalará todo bajo `$HOME/local` en lugar de `/usr/local`.

## Uso
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
o
```sh
$ source /usr/local/bin/tsocks on 
$ telnet example.org
```
o
```sh
$ . /usr/local/bin/tsocks on 
$ telnet example.org
```

## Notas para macOS

* Instalar OpenSSH desde fuentes (o usar Homebrew https://brew.sh puerto) ya que el ssh predeterminado no funcionará con la biblioteca precargada:
```sh
brew install openssh
```

* Para sockificar permanentemente todas las conexiones usando la biblioteca precargada, establecer las variables de entorno esenciales al iniciar sesión:
```sh
launchctl setenv DYLD_FORCE_FLAT_NAMESPACE 1
launchctl setenv DYLD_INSERT_LIBRARIES /usr/local/lib/libtsocks.dylib
```

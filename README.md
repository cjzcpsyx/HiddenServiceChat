# HiddenServiceChat
Use a Tor hidden service to rin an anonymous chat room.

### Dependency setup
```
cd
wget https://sourceforge.net/projects/levent/files/libevent/libevent-2.0/libevent-2.0.22-stable.tar.gz
wget https://www.torproject.org/dist/tor-0.2.6.10.tar.gz
tar xzvf libevent-2.0.22-stable.tar.gz
cd libevent-2.0.22-stable
./configure --prefix=$HOME/usr --disable-shared --enable-static --with-pic
make
make install
cd
tar xzvf tor-0.2.6.10.tar.gz
cd tor-0.2.6.10
./configure --prefix=$HOME/usr --enable-static-libevent
make
make install
```
At this point you should be able to bootstrap Tor by running
```
~/usr/bin/tor
```
Press Ctrl-­C to exit.

### Disable TLS
To run a server with --disable-tls option
```
./server --disable-tls 127.0.0.1 5280
```
To run Tor using the hidden service configuration
```
~/usr/bin/tor -f server-torrc
```
To connect a client
```
./client --disable-tls --socks-port 9150 yoursite.onion 5280
```
NOTICE: the port number "5280" and socks port "9150" and "yoursite.onion" is different among different settings, consult server-torrc file and hs-chat-dir/hostname to figure out.

### Enable TLS
with --tls-cert option
```
./server --tls-cert my.crt --tls-key my.key 127.0.0.1 5280
./client --tls-trustfile ca.crt --socks-port 9150 yoursite.onion 5280
```

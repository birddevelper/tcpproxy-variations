## C++ TCP Proxy Server

### INTRODUCTION
The  C++ TCP  Proxy Server  Variations are  a series  of very  simple
variations made upon the baseline version of the C++ TCP Proxy  server
so as  to demonstrate  how one  can easily  add interesting and useful
functionality  to  the  proxy  server and  also  to  provide  a simple
tutorial on the  usage of the  ASIO library. The  variations presented
are as follows:

- Multi-threaded I/O service
- Limiting of upstream data flow
- Logging of upstream and downstream data flows
- Limiting the number of concurrent client connections


### COPYRIGHT NOTICE
Free use of the C++ TCP Proxy Server variations is permitted under the
guidelines and  in accordance  with the MIT License.

http://www.opensource.org/licenses/MIT


### DOWNLOADS & UPDATES

All updates and the  most recent version of  the C++ TCP Proxy  Server
variations can be found at:
http://www.partow.net/programming/tcpproxy/index.html

Code repository:
https://github.com/ArashPartow/tcpproxy-variations



### COMPILATION
- For a complete build: make clean all
- To strip executables: make strip_bin


### COMPILER COMPATIBILITY
- GNU Compiler Collection (4.3+)
- Intel® C++ Compiler (9.x+)
- Clang/LLVM (1.1+)
- Microsoft Visual Studio C++ Compiler (8.1+)



### Excutable Binaries
- Linux : tcpproxy_server_linux_binaries.zip
- Windows : tcpproxy_server_win32_binaries.zip


### How to use 


![scenario](http://www.partow.net/images/tcpproxy_server_diagram.png)




A simple scenario is as follows: 

There exists a server at 192.168.0.100 that accepts connections on port 20000, however due to firewall rules external clients can only access a host at 192.168.20.200 on port 8080 (eth0), which coincidentally has access to the 192.168.0 network segment via a second NIC (eth1). A solution for allowing the external clients access to the server is to run the TCP proxy server on the host at 192.168.0.200 with the following configuration:

```bash
tcpproxy_server 192.168.20.200 8080 192.168.0.100 20000
```

The above command when run upon the proxy machine at 192.168.20.200, will bind to port 8080 on eth0 in order to accept connections from external clients - which presumbly will originate from the firewall. Upon a new client connecting, the proxy will make a connection on behalf of the client to the server residing at 192.168.0.100 on port 20000 via eth1, and then proceed to send all incoming data from the client to the server and vice versa. Once either party (client or server) disconnects, the proxy will immediately disconnect the other party.

# ENE419 - Computer Networks - Assignment 2

> Stanislas Lange - 9319520196

1. To determine the IP address of the HTTP service, the client has to use the Domain Name System (DNS) protocol which is an application layer protocol. This protocol runs on top of the transport layer protocol UDP (User Datagram Protocol ).

2. `tcpserver.py`:

```py
from socket import *

serverPort = 12000
serverSocket = socket(AF_INET,SOCK_STREAM)
serverSocket.bind(('',serverPort))
serverSocket.listen(1)
print('The server is ready to receive')

while True:
    connectionSocket, addr = serverSocket.accept()
    sentence = connectionSocket.recv(1024)
    print(sentence.decode(encoding="utf-8", errors="strict"))
    connectionSocket.close()
```

Sample output by accessing `http://localhost:12000` from Chrome on macOS:

```
The server is ready to receive
GET / HTTP/1.1
Host: localhost:12000
Connection: keep-alive
DNT: 1
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/78.0.3904.97 Safari/537.36
Sec-Fetch-User: ?1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3
Accept-Encoding: gzip, deflate, br
Accept-Language: en-GB,en-US;q=0.9,en;q=0.8,fr-FR;q=0.7,fr;q=0.6,ko-KR;q=0.5,ko;q=0.4
```

3. Yes, if the sender sends some packets and times out before receiving the receiver's ACKs, he will send the packets again and the receiver will re-ACK. The sender will receive the first set of ACK so it will move on to the next packets. But then it will receive the second set of ACKs for the first set of packets which thus falls outside of its current window.

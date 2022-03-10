# Network

### OSI
* Application (HTTP)
* Presentation
* Session
* Transport (TCP)
* Network
* Data link
* Physical

### TCP
#### TCP vs UDP
- TCP is a connection-oriented protocol, whereas UDP is a connectionless protocol.
- UDP
    - broadcasting: server side keeps sending, don't care client received it or not
    
| Basis | Transmission control protocol (TCP) | User datagram protocol (UDP) |
| --- | --- | --- |
| Type of Service | TCP is a connection-oriented protocol. Connection-orientation means that the communicating devices should establish a connection before transmitting data and should close the connection after transmitting the data. | UDP is the Datagram-oriented protocol. This is because there is no overhead for opening a connection, maintaining a connection, and terminating a connection. UDP is efficient for broadcast and multicast types of network transmission. |
| Reliability | TCP is reliable as it guarantees the delivery of data to the destination router. | The delivery of data to the destination cannot be guaranteed in UDP. |
| Error checking mechanism | TCP provides extensive error-checking mechanisms. It is because it provides flow control and acknowledgment of data. | UDP has only the basic error checking mechanism using checksums. |
| Acknowledgment | An acknowledgment segment is present. | No acknowledgment segment. |
| Sequence | Sequencing of data is a feature of Transmission Control Protocol (TCP). this means that packets arrive in order at the receiver. | There is no sequencing of data in UDP. If the order is required, it has to be managed by the application layer. |
| Speed | TCP is comparatively slower than UDP. | UDP is faster, simpler, and more efficient than TCP. |
| Retransmission | Retransmission of lost packets is possible in TCP, but not in UDP. | There is no retransmission of lost packets in the User Datagram Protocol (UDP). |
| Header Length | TCP has a (20-60) bytes variable length header. | UDP has an 8 bytes fixed-length header. |
| Weight | TCP is heavy-weight. | UDP is lightweight. |
| Handshaking Techniques | Uses handshakes such as SYN, ACK, SYN-ACK | It’s a connectionless protocol i.e. No handshake |
| Broadcasting | TCP doesn’t support Broadcasting. | UDP supports Broadcasting. |
| Protocols | TCP is used by HTTP, HTTPs, FTP, SMTP and Telnet. | UDP is used by DNS, DHCP, TFTP, SNMP, RIP, and VoIP. |
| Stream Type | The TCP connection is a byte stream. | UDP connection is message stream. |
| Overhead | Low but higher than UDP. | Very low. |

#### TCP 3-Way Handshake Process
- Step 1 (SYN): In the first step, the client wants to establish a connection with a server, so it sends a segment with SYN(Synchronize Sequence Number) which informs the server that the client is likely to start communication and with what sequence number it starts segments with
- Step 2 (SYN + ACK): Server responds to the client request with SYN-ACK signal bits set. Acknowledgement(ACK) signifies the response of the segment it received and SYN signifies with what sequence number it is likely to start the segments with
- Step 3 (ACK): In the final part client acknowledges the response of the server and they both establish a reliable connection with which they will start the actual data transfer

- Send payload: SerialNumber length, data payload
- ACK = SerialNumber + length <-> next SerialNumber

#### TCP Connection Termination
- Step 1 (FIN From Client) – 
Suppose that the client application decides it wants to close the connection. (Note that the server could also choose to close the connection). This causes the client to send a TCP segment with the FIN bit set to 1 to the server and to enter the FIN_WAIT_1 state. While in the FIN_WAIT_1 state, the client waits for a TCP segment from the server with an acknowledgment (ACK).
- Step 2 (ACK From Server) – 
When the Server received the FIN bit segment from Sender (Client), Server Immediately sends acknowledgement (ACK) segment to the Sender (Client).
- Step 3 (Client waiting) – 
While in the FIN_WAIT_1 state, the client waits for a TCP segment from the server with an acknowledgment. When it receives this segment, the client enters the FIN_WAIT_2 state. While in the FIN_WAIT_2 state, the client waits for another segment from the server with the FIN bit set to 1.
- Step 4 (FIN from Server) – 
The server sends the FIN bit segment to the Sender(Client) after some time when the Server sends the ACK segment (because of some closing process in the Server).
- Step 5 (ACK from Client) – 
When the Client receives the FIN bit segment from the Server, the client acknowledges the server’s segment and enters the TIME_WAIT state. The TIME_WAIT state lets the client resend the final acknowledgment in case the ACK is lost. The time spent by clients in the TIME_WAIT state depends on their implementation, but their typical values are 30 seconds, 1 minute, and 2 minutes. After the wait, the connection formally closes and all resources on the client-side (including port numbers and buffer data) are released.

### HTTP
HTTP is using TCP/IP protocol and restrict the communication in request-response model

- Request
    - Methods (GET, POST, DELETE, PUT,..) | what to do
    - Header (Metadata about the request)
        - cookies: prevent web attack (robot keeps clicking button) generate token, put in the cookies, contains security information.
    - Body (contains data in text and binary format) only POST and PUT allows body
- Response
    - Status Code( 2xx success,3xx redirect,4xx client error,5xx server error) 
    - Header
    - Body

#### Get vs Post 
- GET requests are often used for fetching documents
- POST parameters are often used for updating data for actually making changes to the server (or) to the data held on the server
    
#### Patch vs Post vs PUT
- POST is always for creating a resource ( does not matter if it was duplicated ) PUT is for checking if resource exists then update, else create new resource. PATCH is always for updating a resource.
- POST non-idempotent
- A request method is considered **idempotent** if the intended effect on the server of multiple identical requests with that method is the same as the effect for a single such request

### Spring Web MVC Annotations
- [TBD](https://springframework.guru/spring-framework-annotations/)
    - 


    
 


 





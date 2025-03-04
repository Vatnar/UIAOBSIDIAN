# 
## Exercise 1 (R3)
- For a communication session between a pair of processes, which process is the client and which is the server?
The client is the process that initiates communication  with a request to the other process. The server is the process that patiently waits for a request and then proceeds to formulate a response. 
## Exercise 2 (R5)
- What information is used by a process running on one host to identify a process running on another host?
An IP-address (internet protocol address) is used for identifying another host. To identify what process on that host a port number is used, since a host can run multiple services/processes at once that communicate over the internet. 
## Exercise 3 (R12)
- How can websites keep track of users? Do they always need to use cookies?
A website often contain a database where they keep track of users using cookies (unique identifiers). When a user first accesses a website using the HTTP (hypertext transfer protocol) the website generates a cookie for the user, which it sends back so the user can use the next time to be identified. The reason websites often use cookies is because HTTP is stateless. 

Websites are not required to use cookies, they can also use session storage, lopcal storage, IP Adresses, user authentication tokens or fingerprinting techniques to track users. 
## Exercise 4 (R16)

- Suppose Alice, with a Web-based e-mail account (such as Hotmail or Gmail), sends a message to Bob, who accesses his mail from his mail server (using POP or IMAP). Discuss how the message gets from Alice’s host to Bob’s host. Be sure to list the series of application-layer protocols that are used to move the message between the two hosts.
First Alice fills out the header values of the email along with a message body. The message gets transmitted from the UA (user agent or mail program) to her mail server using SMTP (simple mail transfer protocol). The message gets added to the send queue on the mail server and transmitted onwards to bobs mail server. Bob then uses either IMAP (Internet message access protocol) or (post office protocol) to fetch the message from his mail server and display it in his UA. 

IMAP allows bob to access and manage his email while keeping them stored on the server, but POP3 downloads the email to bobs device and deletes them from the server.

## Exercise 5 (R18)

- What is the HOL blocking (“først-i-køen”-blokkering) issue in HTTP/1.1? How does HTTP/2 attempt to solve it?
Head-of-line blocking references problems with retrieving different sized objects using the HTTP GET method. in HTTP/1.1 the server treats HTTP GET methods using FCFS (FIRST COME FIRST SERVED) scheduling, and always returns the object first specified first. Lets say the first object is a big image file, then the smaller HTML file would have to wait. In HTTP/2 objects are retrieved based on a client-defined priority. This can be why you often see text being rendered before images on websites.

**Exercise 6 (P4)**

- Consider the following string of ASCII characters that were sent when the browser sent an HTTP GET message (i.e., this is the actual content of an HTTP GET message). Answer the following questions, indicating where in the HTTP GET message below you find the answer.

```HTTP
GET /cs453/index.html HTTP/1.1
Host: gaia.cs.umass.edu
User-Agent: Mozilla/5.0 (Windows;U; Windows NT 5.1; en-US; rv:1.7.2) Gecko/20040804 Netscape/7.2 (ax)
Accept:ext/xml, application/xml, application/xhtml+xml, text/html;q=0.9, text/plain;q=0.8,image/png,*/*;q=0.5  
Accept-Language: en-us,en;q=0.5
Accept-Encoding: zip,deflate
Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.7
Keep-Alive: 300
Connection:keep-alive  
_<cr><lf>       (empty line)
```

A. What is the URL of the document requested by the browser?
B. What version of HTTP is the browser running?
C. Does the browser request a non-persistent or a persistent connection?
D. What is the IP address of the host on which the browser is running?
E. What type of browser initiates this message? Why is the browser type needed in an HTTP request message?

A) The URL of the document requested by the browser is http://gaia.cs.umass.edu/cs453/index.html, we can find this by combining the name of the host with the relative location int  the GET method. The url consists of a hostnmame and a path.
B) In the GET method we can observe: HTTP/1.1 meaning that the browser is using version 1.1
C) The browser does request a persistent connection which we can deduce based on the penultimate line; keep-alive. 
D) The IP adress of the host of the browser is not explicitely stated. The IP Address of the host can be found using DNS resolution and not contained within the HTTP message
E) The browser that initiates this message is Mozilla Netscape, this is needed because the website might produce different output based on what platform or browser requests the information.

## Exercise 7 (P18)

1. What is a _whois_ database?
   A internet reccord listing that identifieswho owns a domain and how to get in contact with them. ICANN regulated.
2. Use a _whois_ databases on the Internet to obtain the names of two DNS servers (_for eksempel navneserverne til_ uia.no). Indicate which _whois_ databases you used.
   Used who.is database and searched for uia.no. There are three listings for name servers, being ns2.uia.no, ns1.uia.no and nn.uninett.no
   
3. Use _nslookup_ on your local host to send DNS queries to three DNS servers: your local DNS server and the two DNS servers you found in part (b). Try querying for Type A, NS, and MX reports. Summarize your findings.
   ![[2025.01.30.11.57.33.705 WindowsTerminal.jpg]]
   non authrorative
4. Use _nslookup_ to find a Web server that has multiple IP addresses. Does the Web server of your institution (school or company) have multiple IP addresses?#

## Exercise 8 (P22)
 
- **Ch. 2.6 (30 points)**. Consider distributing a file of **_F_** = 500 MB to N peers, where M is SI standard (base 10) $10^6$ and not binary (base 2) $2^{20}$ = 10242. The server has an upload rate of $u_s$ = 1000 Mbps, and each peer has a download rate of $d_i$ = 80 Mbps (i.e., $d_{min}=d_{i}$) and an upload rate of $u_{i}$. For **_N_** = 15, 300, and 6 000 and $u_i$ = 2 Mbps, 10 Mbps, and 50 Mbps, prepare a table giving the minimum distribution time for each of the combinations of **_N_** and $u_i$ for both client-server distribution and P2P distribution.
### Client Server

$F = 500\;MB$, $d_{i} = 80\;Mbps$, $u_{s}=1000\;Mbps$. 

The load for the upload rate of the server would be $N\cdot d_{i}$ as long as its less than $u_s$. 
So for a file with size $F = 500\;MB=4000\;Mb$ it would take  minimum of $F/d_{i}$. 
$u_s/d_{i}=12.5$. Therefore all our values of N exceed the limit for downloading at the max speed at the same time. As long as the full upstream capacity of the server is reached its the same if all clients download slower at the same time or a few at at time.

$$u_{s}/15= 66.67\;Mbps\qquad \frac{4000\;Mb}{66.67\;Mbps} \approx60s$$
$$u_{s}/300= 3.33\;Mbps\qquad \frac{4000\;Mb}{3.33\;Mbps} \approx1201s\approx 20m$$
$$u_{s}/6000= 0.1667\;Mbps\qquad \frac{4000\;Mb}{0.1667\;Mbps} \approx23995s\approx6.6t$$

Peer upload rate does not matter here, unless a peer first should upload the file, then just add $F/u_i$ to the minimum time.

| Minimum Distribution Time | $N$     |
| ------------------------- | ------- |
| $60s$                     | $15$    |
| $20m$                     | $300$   |
| $6.6t$                    | $6 000$ |
### P2P
The total download bandwhitdh available to a peer depends on the number of other peers.
$$B_{total}=\frac{(N-1)\cdot u_{i}}{N}$$
But max $d_i$. 

$$B_{N=15,U_{i}=2}=\frac{(15-1)\cdot 2}{15}=1.86 < D_{i}$$
$$B_{N=15,U_{i}=10}=\frac{(15-1)\cdot 10}{15}=9.33 < D_{i}$$
$$B_{N=15,U_{i}=50}=\frac{(15-1)\cdot 50}{15}=46 < D_{i}$$
$$B_{N=300,U_{i}=2}=\frac{(300-1)\cdot 2}{300}=1.99 < D_{i}$$
$$B_{N=300,U_{i}=10}=\frac{(300-1)\cdot 10}{300}=9.96 < D_{i}$$
$$B_{N=300,U_{i}=50}=\frac{(300-1)\cdot 50}{300}=49.8 < D_{i}$$
$$B_{N=6000,U_{i}=2}=\frac{(6000-1)\cdot 2}{6000}=1.999 < D_{i}$$
$$B_{N=6000,U_{i}=10}=\frac{(6000-1)\cdot 10}{6000}= 9.999< D_{i}$$
$$B_{N=6000,U_{i}=50}=\frac{(6000-1)\cdot 50}{6000}=49.99 < D_{i}$$

| Minimum Distribution Time | $N$        | $u_i$          |
| ------------------------- | ---------- | -------------- |
| 2150s                     | $15$       | $2\;Mbps$      |
| 428s                      | $15$<br>   | $10\;Mbps$<br> |
| 86s                       | $15$<br>   | $50\;Mbps$<br> |
| 2010s                     | $300$<br>  | $2\;Mbps$<br>  |
| 401s                      | $300$      | $10\;Mbps$     |
| 80s                       | $300$<br>  | $50\;Mbps$<br> |
| 2005s                     | $6000$<br> | $2\;Mbps$<br>  |
| 410s                      | $6000$<br> | $10\;Mbps$<br> |
| 80s                       | $6000$<br> | $50\;Mbps$<br> |
We can see how P2P file distribution scales way better than using a server. As N approaches infinity the download time approaches $F/u_i$. 
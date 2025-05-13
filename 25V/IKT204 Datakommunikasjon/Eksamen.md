SEQ = Previous packed , SEQ + payload size
ACK = received packet SEQ + payload size

SEQ random first
Stop and wait vente på ACK
dårlig utnyttelse

pipelining
instead of  waiting for ack, send continuously 
Server responds with ack of the packet its waiting for. 

TCP has 3 error handling mechanisms
- Timer
	- Timeout. 
- Cumulative ACK
	- If an ack is lost, client can see that the server responds for the next one. 
- Fast Transmit
	- Resends old ack value, duplicate ACKS. If 3 duplicate ACKS resend data.
	- If timers times out then its sent because of the timer instead.
	- After fast transmit can be selective ack or cumulative ack on this one
- Fast transmit pipelining
	- 
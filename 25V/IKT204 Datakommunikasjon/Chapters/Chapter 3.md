```table-of-contents
```
# Principles of reliable data transfer
Reliable data transfer protocol has the responsibility of providing a service abstraction of a reliable tunnel. Its hard cause e.g. TCP is a **reliable data transfer protocol** that is implemented on top of an unreliable IP end-to-end network layer.
![[Pasted image 20250221095707.png]]

Reliable data transfer over a channel with bit errrors.

Use **ARQ** (**Automatic Repeat reQuest**) protocols: positive acks (OK), negative acks (repeat).
- **Error detection**. UDP uses **checksum** for instance. 
- **receiver feedback**. positive **ACK** or  negative **NAK**
- **Retransmission.** A packet that has received an error will be retransmitted by sender.
![[Pasted image 20250221100828.png]]
When the protocol is waiting for acknowledgenment it cnanot send new data, therefore this protocol is called **stop and wait.** 
Our protocol has not accounted for corruption ack and NAK, therefore checksums need to be added to these.

Three possibilituies to handle corrujpted ACKs or NAKs:
- what did you say? can lead to new corrupted stuff. 
- add enough cheksum bits that the sender can not only detect but also recover errors.
- Just make the sender resend the current data packet when it receives a garbled ACK or NAK. It does introduce *duplicate packets*. But then the receiver wont know if its a retransmission or new data. 

The solution used in most of these protocols including TCP is to add a *sequence number*. If the receiver get an already used sequence number. For a  stop and wait protocol a 1 bit sequence number will suffice, basically a Boolean that says if its a new or an old packet. 
![[Pasted image 20250221102050.png]]
![[Pasted image 20250221102101.png]]
Instead of sending NAK we send ACK for the last correctly received packet. **Duplicate ACKs** then the sender knows then the sender knows that the packet following the duplicate ACKs was not received properly. 
![[Pasted image 20250221102354.png]]
![[Pasted image 20250221102656.png]]

*How to detect packet loss and what to do*
Use a *countdown timer* to retransmit a packet if not received ACK within so so long. 
![[Pasted image 20250221102819.png]]
	Rdt3.0 is sometiems know as the alternating-bit-protocl since packet sequence nubmers alternate between 0 and 1. 
## Pipelining
Because rdt3.0 is a stop and wait protocol people would be unhappy about performance.ø 
![[Pasted image 20250221103003.png]]
![[Pasted image 20250221103034.png]]
![[Pasted image 20250221103040.png]]

Consider RTT of 30ms.  with transmission rate R of 1 Gbps, packet size 1 KB, including header and data, the tiem to transmit woudl be 8 microseconds. 

t=RTT/2+L/R = 15.008 msec, ack gets back to sender at 30msec. The sender sends at 30.008 msec. we define the *utilization* of the sender as the fraction of time the sender is actually busy which gives us. $U_{sender}=\frac{L}{R} * RTT + \frac{L}{R} = 0.00027$ or 0.027%. I.e using 267kbs on a Gbps link. 

Rather pipeline
- Sequence numbers must be increased, since each in transit packet  (not counting retransmissions) must have a unique sequence  number and there may be multiple unacknowlegded packets.
- Sender and receiver must buffer packets. Sender must at least buffer unacknowledged packets. Bufferinc correctly received packets may be needed by receiver. 
- Sequence and buffering needs is decided by which pipelined error recovery approach: *Go-Back-N* and *Selective repeat*.

### Go-Back-N
The sender can send multiple packets before getting ACKS. but is constrained to  max N of unACKed packets in the pipeline. 
Sliding window protocol


![[Pasted image 20250221103239.png]]
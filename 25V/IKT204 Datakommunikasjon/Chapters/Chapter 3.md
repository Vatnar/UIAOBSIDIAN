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
*How to detect packet loss and what to do*

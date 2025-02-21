```table-of-contents
```
# Principles of reliable data transfer
Reliable data transfer protocol has the responsibility of providing a service abstraction of a reliable tunnel. Its hard cause e.g. TCP is a reliable data transfer protocol that is implemented on top of an unreliable IP end-to-end network layer.
![[Pasted image 20250221095707.png]]

Reliable data transfer over a channel with bit errrors.

Use ARQ (Automatic Repeat reQuest) protocols: positive acks (OK), negative acks (repeat).
- Error detection. UDP uses checksum for instance. 
- receiver feedback. positive ACK or  negative NAK
- Retransmission. A packet that has received an error will be retransmitted by sender.
![[Pasted image 20250221100828.png]]
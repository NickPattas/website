*Capability-based security* is a concept in the design of secure computing systems, **one of the existing security models**.

A `capability` (known in some systems as a` key`) is a `communicable`, `unforgeable` *token of authority*. It refers to a value that references an object along with an associated set of access rights. A user program on a *capability-based operating system* must use a capability to *access an object*.

Capability-based security refers to the principle of designing user programs such that they directly share capabilities with each other according to the principle of `least privilege`, and to the operating system infrastructure necessary to make such *transactions efficient and secure*. 

Capability-based security is to be contrasted with an approach that uses traditional `UNIX permissions and access control lists`.

Although most operating systems implement a facility which resembles capabilities, they typically **do not provide enough support to allow for the exchange of capabilities among possibly mutually untrusting entities to be the primary means of granting and distributing access rights throughout the system.**
A capability-based system, in contrast, is designed with that goal in mind.
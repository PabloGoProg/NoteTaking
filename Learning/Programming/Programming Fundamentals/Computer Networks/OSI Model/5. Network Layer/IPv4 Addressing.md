IPv4 Addressing is a system of _unique 32-bit numerical identifiers_ assigned to devices on a network to enable communication.

```
2^8 - 00000000 - Octet
4 Octets = 1 IPv4

Dot Separated Format -> [1 Octet].[2 Octet].[3 Octet].[4 Octet]
```

With the structure of IPv4 addressing we can create _2³² possible different IPs_. But those 32 bits are not treated as one flat list of isolated addresses. _They are divided into a network portion and a host portion_ so routers can forward packets by network blocks instead of tracking every individual device. _This division makes routing scalable_: the network bits identify where the packet must go, and the host bits identify the specific device inside that network.

---
## Classful Addressing


IPv4 Addressing is a system of _unique 32-bit numerical identifiers_ assigned to devices on a network to enable communication.

```
2^8 - 00000000 - Octet
4 Octets = 1 IPv4

Dot Separated Format -> [1 Octet].[2 Octet].[3 Octet].[4 Octet]
```

With the structure of IPv4 addressing we can create _2³² possible different IPs_. But those 32 bits are not treated as one flat list of isolated addresses. _They are divided into a network portion and a host portion_ so routers can forward packets by network blocks instead of tracking every individual device. _This division makes routing scalable_: the network bits identify where the packet must go, and the host bits identify the specific device inside that network.

---
## Classful Addressing

Classful Addressing is is ==an obsolete IPv4 networking architecture that divides IP addresses into five fixed, rigid classes (A, B, C, D, and E) based on leading bits.== 

- _Class A_: 8 bit for Network IDs (NID) and 24 for Host IDs (HID).
	- Range from 0.0.0.0 to 127.255.255.255.
	- First Bits: `0`
- _Class B_: 16 bit for Network IDs (NID) and 16 for Host IDs (HID).
	- Range from 128.0.0.0 to 191.255.255.255.
	- First Bits: `10`
- _Class C_: 24 bit for Network IDs (NID) and 8 for Host IDs (HID).
	- Range from 192.0.0.0 to 223.255.255.255.
	- First Bits: `110`
- _Class D_:
	- Range from 224.0.0.0 to 239.255.255.255.
	- First Bits: `1110`
- _Class E_: 
	- Range from 240.0.0.0 to 255.255.255.255.
	- First Bits: `1111`

> There's one issue with Classful Addressing: the IP waste. Fro example, if we only need a 1000 IPs, we can't use Class C because it only provides 254 IPs, so we are forced to use a Class B division, but class B provides 65,534 IPs in the subset, leading to the waste of a big number of IPs.

---
## Class A-E Addressing Deep Dive

In classful IPv4 addressing, some network and host values are reserved and cannot be assigned as normal addresses. A network field with all bits set to 0 was reserved to mean “this network”, and the Class A block `127.0.0.0/8` was reserved for loopback testing. For example, `127.0.0.1` refers to the local machine itself.

The same principle applies to the host portion of an address. A host field with all bits set to 0 identifies the network address, while a host field with all bits set to 1 identifies the broadcast address for that network. Therefore, these two host values are not assigned to individual devices.

---
### Class A

- **Structure**: `[ 8 bit for NID ] . [ 24 bit for HID ]`
- **Fixed Start**: `0`
- **Possible Networks**: $2^7$ -> 8 bits of NID minus 1 fixed bit.
- **NID Range**:
	- Overall -> `0[0000000 - 1111111]` (0, 127)
	- Available for Assign -> `00000001 - 01111110` (1, 126)
	- Reserved:
		1. `0.X.X.X` -> DHCP Client
		2. `127.X.X.X` -> Lookback Testing
- **HID Range**:
	- Overall -> `0XXXXXXX.[ 24 bit ]` ($2^{24}$)
	- Available for Assign -> $2^{24} - 2$
	- Reserved:
		1. `X.0.0.0` -> Identifies the network itself.
		2. `X.255.255.255` -> Broadcast Address.

### Class B

- **Structure**: `[ 16 bit for NID ] . [ 16 bit for HID ]`
- **Fixed Start**: `10`
- **Possible Networks**: $2^{14}$ -> 16 bits of NID minus 2 fixed bits.
- **NID Range**:
	- Overall: `128.0.0.0` to `191.255.0.0`
	- Available for assignment: all Class B network IDs in the classful model, because the fixed prefix 10 prevents the NID from being all zeroes or all ones.
	- Reserved:
	    - No Class B network is reserved for DHCP client in the same way as `0.0.0.0/8`.
	    - No Class B network is reserved for loopback testing in the same way as `127.0.0.0/8`.
- **HID Range**:
	- Overall: 16 bits, $2^{16}$ possible host values per network.
	- Available for assignment: $2^{16} - 2$ = 65,534 usable hosts.
	- Reserved:
	    - Host bits all 0: identifies the network itself.
	    - Host bits all 1: identifies the broadcast address.

### Class C

- Structure: `[ 24 bits for NID ] . [ 8 bits for HID ]`
- Fixed Start: `110`
- Possible Networks: $2^{21}$, because the NID has 24 bits, but the first 3 bits are fixed.
- NID Range:
    - Overall: `192.0.0.0` to `223.255.255.0`
    - Available for assignment: all Class C network IDs in the classful model, because the fixed prefix `110` prevents the NID from being all zeroes or all ones.
    - Reserved:
        1. No Class C network is reserved for DHCP client in the same way as `0.0.0.0/8`.
        2. No Class C network is reserved for loopback testing in the same way as `127.0.0.0/8`.
- HID Range:
    - Overall: 8 bits, $2^8$ possible host values per network.
    - Available for assignment: $2^8 - 2$ = 254` usable hosts.
    - Reserved:
        1. Host bits all `0`: identifies the network itself.
        2. Host bits all `1`: identifies the broadcast address.

### Class D

- Structure: Class D does not use the classic `[ NID ] . [ HID ]` structure.
- Fixed Start: `1110`
- Range:
    - Overall: `224.0.0.0` to `239.255.255.255`
- Purpose:
    - Used for multicast addresses.
    - A multicast address identifies a group of receivers, not a single host and not a normal network.
- Possible Addresses:
    - $2^{28}$, because the first 4 bits are fixed as `1110`.
- Available for normal host assignment:
    - None.
    - Class D addresses are not assigned to individual devices as unicast IPs.
- Reserved behavior:
    1. No network address with host bits all `0`.
    2. No broadcast address with host bits all `1`.
    3. No DHCP-client block equivalent to `0.0.0.0/8`.
    4. No loopback block equivalent to `127.0.0.0/8`.

### Class E

- Structure: Class E does not use the classic `[ NID ] . [ HID ]` structure.
- Fixed Start: `1111`
- Range:
    - Overall: `240.0.0.0` to `255.255.255.255`
- Purpose:
    - Reserved for experimental or future use in the classful model.
    - It is not used for normal unicast host assignment.
- Possible Addresses:
    - $2^{28}$, because the first 4 bits are fixed as `1111`.
- Available for normal host assignment:
    - None.
- Reserved behavior:
    1. No network address with host bits all `0`.
    2. No broadcast address with host bits all `1`.
    3. No DHCP-client block equivalent to `0.0.0.0/8`.
    4. No loopback block equivalent to `127.0.0.0/8`.

Important detail:

`255.255.255.255` is inside the Class E range by bit pattern, but it has a special meaning. It is the limited broadcast address, used to send a packet to all hosts on the local network segment.

So:

`255.255.255.255` is not assigned to a host.

It is not a normal Class E host address.
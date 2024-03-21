---
title: "IPv6 mechanism for determining source and destination address pairs"
abbrev: "IPv6 Get Address Pairs"
category: std

docname: draft-nb-6man-getv6apr-latest
submissiontype: IETF  # also: "independent", "editorial", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
area: "Internet"
workgroup: "IPv6 Maintenance"
keyword:
 - next generation
 - unicorn
 - sparkling distributed ledger
venue:
  group: "IPv6 Maintenance"
  type: "Working Group"
  mail: "ipv6@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/ipv6/"

author:
      -
        ins: N. Buraglio
        name: Nick Buraglio
        org: Energy Sciences Network
        email: buraglio@forwardingplane.net

normative:
  RFC2119:
  RFC4193:
  RFC7078:
  RFC7526:
  RFC8925:
informative:
  RFC6724:

--- abstract

This provides a comprehensive mechanism for determining a "best use" source address / destination address (SA/DA) pair for IPv6 connections and is intended to be a modernized replacement for existing SA/DA algorithms such as socket.getaddrinfo(). Instead of the current methodology of returning a list of destination addresses, this returns a list of source and destination address pairs, which are evaluated based on pre-determined and potentially user defined criteria. This mitigates the problem of the operating system choosing an inappropriate source address, as can occur with legacy mechanisms.

--- middle

# Introduction

With the rapid expansion of IPv6 and the building momentum of retiring IPv4 as a protocol, the exposure of limits of current implementations of IPv6 source and destination address selection has become acutely more apparent.  [RFC6724] has frequently been analyzed and in many cases deemed in need of a refresh, if only to address limits of the emergence of dual-stack and now the removal of IPv4. IPv6 by design supports and employs multiple addresses per interface. Be cause of this feature, there is necessarily a set of heuristics to determine which address to use for a given operation. Thus far, the algorithm has operated well enough to allow for successful deployments and operational supportability. However, it is limited and somewhat inconsistent in the overall implementations across platforms. Because of these limited, and with the evolving reliance internetwork connectivity, the "always connected" expectation of general users, there is a necessary evolution required for continued expansion of the IPv6 protocol as it pertains to host source and address selection.

# Conventions and Definitions

{::boilerplate bcp14-tagged}

SA: Source Address
DA: Destination Address
Dual-Stack: Configuration of a device network interfaces as to originate and understand both IPv4 and IPv6 packets.

# Limitations of Current Implementations

PLACEHOLDER via RFC6724:

```
In this implementation architecture, applications use APIs [10] like
getaddrinfo() that return a list of addresses to the application.
This list might contain both IPv6 and IPv4 addresses (sometimes
represented as IPv4-mapped addresses).  The application then passes a
destination address to the network stack with connect() or sendto().
the application would then typically try the first address in the
list, looping over the list of addresses until it finds a working
address.  In any case, the network layer is never in a situation
where it needs to choose a destination address from several
alternatives.
```

# Proposed

# Example Code

# Security Considerations

TODO Security


# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.

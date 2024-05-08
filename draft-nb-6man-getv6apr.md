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
 - IPv6
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
  GETAPR:
    target: https://github.com/becarpenter/getapr
    title: "Example code repo"
  GETADDRINFO:
    target: https://man7.org/linux/man-pages/man3/getaddrinfo.3.html
    title: "Linux MAN page for getaddrinfo()"

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
Known Local Prefix: A prefix known to be local to the administrative domain of the network the host resides on at a given time.

Known Local Prefix: A prefix known to be local to the administrative domain of the network the host resides on at a given time.


# Current Implementations and Inherent Limitations

Current implementations of SA/DA selection are limited in several notable ways. Current implementations include a lack of definable user control over source and destination address selection pairs, limited or no mechanism for periodic testing of address pairs and no inherent way to support performance and availability of resources. The most common implementations are derived from the getaddrinfo() implementation which returns one or more addrinfo structures, each of which contains an Internet address that can be specified in a call to bind() or connect() as described in [GETADDRINFO].

 via [RFC6724]:

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

## Source address enumeration and availability handling
A given host will have multiple addresses in an environment that support IPv6, and will have multiple addresses in different address families when operating on a dual-stacked network. Because there may exist multiple valid destination addresses returned from any given DNS query, consisting of both IPv6 and IPv4 addresses as well as the potential presence of a known local address that is unique to the particular network locality, a mechanism for enumerating and testing each address pair must exist in order to ensure both appropriate resource use (i.e. using a known local address when operating on the known-local network).

## Active probing
Due to the dynamic nature of internetworking, active probing of destinations in use should be performed to ensure the best possible and most performant destination is cached for use. This active probing includes all destinations returned by a DNS query for a given resource. These targets are stored in a local cache and ranked by best performance as defined by the fastest response time from each source address local to the host.

Probing targets should rotate and be refreshed at a regular interval in order to prevent unintentional oversubscription of both the probe targets and any intermediary links in the path.

## State caching
Each system process should cache the source and destination address pairs in a ranked order for system-wide reference by any application requesting network resources, or by the operating system itself.

## Operating system differences

# Example Code
A working implementation of address pair enumeration, testing, and active probing called [GETAPR] can be found on GitHub here.

```
Add agreed upon code here
```

# Security Considerations

TODO Security


# IANA Considerations

This document has no IANA actions.

--- back

# Acknowledgments
{:numbered="false"}

The authors would like to acknowledge the valuable input from Brian Carpenter

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
area: Int
workgroup: WG Working Group
keyword:
 - next generation
 - unicorn
 - sparkling distributed ledger
venue:
  group: WG
  type: 6MAN
  mail: ipv6@ietf.org
  arch: https://example.com/WG

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


--- abstract

This provides a comprehensive mechanism for determining a "best use" source address / destination address (SA/DA) pair for IPv6 connections and is intended to be a modernized replacement for existing SA/DA algorithms such as socket.getaddrinfo(). Instead of the current methodology of returning a list of destination addresses, this returns a list of source and destination address pairs, which are evaluated based on pre-determined and potentially user defined criteria. This mitigates the problem of the operating system choosing an inappropriate source address, as can occur with legacy mechanisms.

--- middle

# Introduction

TODO Introduction


# Conventions and Definitions

{::boilerplate bcp14-tagged}


# Security Considerations

TODO Security


# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.

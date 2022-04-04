---
title: "SCION Overview"
abbrev: "SCION I-D"
category: info

docname: draft-perrig-scion-overview-latest
v: 3
area: rtg
workgroup: panrg
keyword: Internet-Draft
venue:
  group: WG
  type: Working Group
  mail: WG@example.com
  arch: https://example.com/WG
  github: USER/REPO
  latest: https://example.com/LATEST

author:
 -   ins: A. Perrig
     name: Adrian Perrig
     org: ETH Zuerich
     email: adrian.perrig@inf.ethz.ch

normative:
  RFC0791:
  RFC1653:
  RFC2460:
  RFC4271:
  RFC8200:   



informative:


--- abstract

The Internet has been successful beyond even the most optimistic expectations and is intertwined with many aspects of our society. Unfortunately, the security of today’s Internet is not commensurate with its importance as critical infrastructure. Additionally, the Internet has not primarily been built for high availability in the presence of malicious actors, and recent proposals to improve Internet security and availability have been constrained by the setup of the current architecture.

The next-generation inter-network architecture SCION (Scalability, Control, and Isolation On Next-generation networks) aims to address the above-mentioned issues. SCION was explicitly designed from the outset to offer availability and security by default. The architecture provides route control, failure isolation, and explicit trust information for end-to-end communication. It also enables multi-path routing between hosts.

The document gives a high-level overview of the SCION architecture, including its authentication model and the setup of the control- and data plane. As SCION is already in production use today, we conclude with an overview of SCION deployments.    


--- middle

# Introduction

The Introduction section briefly presents the key concepts of the next-generation Internet architecture SCION. We start this section with an explanation of why we designed SCION in the first place.

The sections after the Introduction provide further insight into SCION's main concepts and features. We complete the document with some concrete case studies where SCION has been applied successfully.


## Why SCION?

Two protocols effectively define today’s Internet architecture: the Internet Protocol (IP) {{RFC8200}}, {{RFC0791}} and the Border Gateway Protocol (BGP) {{RFC4271}}. These protocols have remained virtually unchanged since the standardization of IPv6 {{RFC2460}} and BGP-4 {{RFC1653}} in the 1990s. However, as the Internet continued to expand and needed to accommodate new uses, numerous issues came to light. This section presents a compact overview of the Internet's most salient problems and shortcomings, which together are the reason why we developed SCION: To address these issues in order to make the Internet more secure, reliable, transparent, and efficient.

### Internet Protocol

IP is one of the fundamental protocols of the Internet, as it enables the forwarding of packets between end hosts. Its first major version, IPv4, was specified in 1981 {{RFC0791}} and its (non-backward compatible) successor, IPv6, was introduced in 1998 {{RFC2460}}. IP enables the transmission of packets between a source and a destination along a single path that is opaque from the end host’s perspective. To forward packets, end hosts (as well as routers) do not need a complete path, but only a table to determine the next hop solely based on the destination address. Neither senders nor receivers can typically influence the path that their packets take. This approach is simple, but it also comes with many drawbacks:

**Lack of transparency and control**

Being able to select and verify the path that packets take is desirable in many situations. End hosts might want to avoid packets being routed through adversarial or untrusted networks, or they might want to choose the most suitable path with regard to a specific metric (e.g., latency or bandwidth). Unfortunately, IP does not offer such an option. Although systems that enable loose and strict source routing have been proposed, these extensions are not commonly supported in today’s networks. It is also not possible to simultaneously use multiple distinct paths towards the same destination—even though multipath communication offers numerous benefits, which we will encounter throughout the book.

**Stateful routers**

IP routers maintain forwarding tables to determine the next hop of a received packet. This basic requirement has undesirable consequences. Performing a forwarding-table lookup for every packet is a time-consuming operation. Therefore, high-performance networking equipment typically relies on ternary content-addressable memory (TCAM) hardware, which is expensive and energy-intensive. Moreover, the constantly growing size of forwarding tables, partially due to the slow but steady deployment of IPv6, poses a problem for routers, as the storage capacity of TCAM hardware is limited. Routers that keep state for network information can also suffer from denial-of-service (DoS) attacks exhausting the router’s state (460).

### BGP

  - Outages
  - Lack of fault isolation
  - Poor scalability
  - Convergence
  - Single path
  - Lack of security

### General problems

  - Lack of authentication
  - Attack

### Problems with RPKI and BGPsec


### Answer

Solutions should be/have:

- Available in the presence of adversaries
- Transparent and controllable
- Efficient and scalable
- Extensible and algorithm agile
- Deployable
- Formally verifiable

## Key Concepts

### Network Structure and Naming

SCION organizes existing ASes into groups of independent routing planes, called isolation domains (ISDs), which interconnect to provide global connectivity. Isolation domains provide natural isolation of routing failures and misconfigurations, give endpoints strong control over both inbound and outbound traffic, provide meaningful and enforceable trust, and enable scalable routing updates with high path-freshness.

As a path-based architecture, SCION end hosts learn about available network path segments, and combine them into end-to-end paths that are carried in packet headers. SCION also enables multi-path communication among end hosts.

SCION reuses the Autonomous Systems (AS) structure, and ensures that network traffic only flows on policy-compliant paths. To achieve scalability and sovereignty, Isolation Domains (ISD) are introduced. An ISD groups ASes that agree on a set of trust roots, called the Trust Root Configuration (TRC). An AS can be a member of multiple ISDs. The ISD is governed by a set of core ASes, which provide connectivity to other ISDs and manage the trust roots. Typically, the 3–10 largest ISPs of an ISD form the ISD’s core.

Routing is based on the <ISD, AS> tuple, agnostic of local addressing. Existing AS numbers are inherited from the current Internet, but a 48-bit namespace allows for additional SCION AS numbers beyond the 32-bit space in use today. Host addressing extends the network address with a local address, forming the <ISD, AS, local address> 3-tuple. The local address is not used in inter-domain routing or forwarding, does not need to be globally unique, and can thus be an IPv4, IPv6, or MAC address, for example.

### Authentication

Control-Plane PKI/TRC

### Control Plane

The SCION control plane discovers and distributes AS-level path
segments. A path segment encodes a network path at the granularity
of inter-domain interfaces on either end of an inter-domain link
connecting two consecutive ASes on a path.
<!-- Constructing interdomain paths at the granularity of inter-AS links increases the
number of available paths and enables optimization of paths with
regard to different criteria. -->

Each end-to-end path consists of up to three path segments: corepath,
up-path, and down-path segments. Core-path segments
refer to path segments containing only core ASes, an up-path
segment is a path segment from a customer (leaf AS) to a provider
(core AS) inside one ISD, and a down-path segment is a path
segment from a provider (core AS) to a customer (leaf AS) inside
an ISD.

To address the suboptimality of hierarchical routing, SCION
introduces peering links and shortcuts.
In a shortcut, a path only contains an up-path and a down-path segment, which can
cross over at a non-core AS that is common to both paths.
Peering links can be added to up- or down-path segments, resulting in an
operation similar to today’s Internet.

Routing (or path segment construction) is conducted hierarchically
on two levels: (1) among all core ASes of all ISDs, which
constructs core-path segments, and (2) within each ISD, which constructs
up- and down-path segments. The path segment construction process
is referred to as beaconing, where a Path-segment
Construction Beacon (PCB) is initiated by core ASes to iteratively construct path segments.
Up- and down-path segments are interchangeable,
simply by reversing the order of ASes in a segment.
The beaconing process in each AS is performed by its beacon server which is
a part of its Control Service (CS), that performs control-plane-related tasks.

Core beaconing is the process of constructing path segments between core ASes.
During core beaconing, a core AS either initiates PCBs or propagates PCBs received from
neighboring core ASes to all other neighboring core ASes.

Intra-ISD beaconing is the second level of the beaconing hierarchy,
which creates path segments from
core ASes to non-core ASes. For this, core ASes create PCBs and
send them to their non-core neighbors (typically customer ASes).
Each non-core AS propagates the received PCBs to its respective
customers. This procedure continues until the PCB reaches an AS
without any customer (leaf AS) and as a result, all ASes receive
path segments to reach the core ASes of their ISD.
Non-core ASes can include their peering links in the PCBs, enabling
valley-free forwarding if both up- and down-path segments
contain the same peering link.

A global path server infrastructure
is used to disseminate path segments. Each AS contains a path
server as a part of the control service. The infrastructure bears
similarities to DNS, where information is fetched on-demand only.
A core AS’s path server stores all the intra-ISD path segments that
were registered by leaf ASes of its own ISD, and core-path segments
to reach other core ASes.

### Data Plane

Name resolution in SCION returns the <ISD, AS, local address> 3-tuple.
Core- and down-path segments are fetched based on the <ISD, AS> tuple.
Hosts can then combine one of their up-path segments
with the received core- and down-path segments.

Shortcut paths that avoid a core AS are possible, if the up- and down-path contain
the same AS, or if a peering link is available between an AS in the
up-path and an AS in the down-path segment. Cryptographic protections
ensure authentic path segments and prevent unauthorized path combinations.

The path segments contain compact hop-fields, that encode
information about which interfaces may be used to enter and leave
an AS. The hop-fields are cryptographically protected, preventing
path alteration. This so-called Packet-Carried Forwarding State
(PCFS) replaces signaling to use a path, ensuring that routers do
not need any local state on either paths or flows.



## Conventions and Definitions

{::boilerplate bcp14-tagged}



> **NOTE**
> Ideally, the following chapters address the questions raised in [RFC 9217](https://www.ietf.org/rfc/rfc9217.html)


# Authentication

From the book v2, use:
chapter 2.2


# Control Plane

From the book v2, use:
chapters 2.1, 2.3, 2.5.


# Data Plane

From the book v2, use:
chapters 2.4, 5.1


# Deployments

*SCI-ED, SSFC, SCIONLab*

From the book v2, use:
chapters 13 introduction (table 13.1), 13.1, 14.1, 15.3, 15.4


# IANA Considerations

This document has no IANA actions.
TODO: It does have IANA actions, specially regarding ISD and AS numbering.


# Security Considerations

The SCION architecture introduces the following security considerations:


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.

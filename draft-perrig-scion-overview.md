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


informative:
  RFC4264:
  RFC0791:
  RFC1653:
  RFC2460:
  RFC4033:
  RFC4271:
  RFC4443:
  RFC5927:
  RFC6480:
  RFC8200:
  RFC8205:
  RFC8446:
  SCHUCHARD2011: DOI.10.1145/1866307.1866411
  CAESAR2005: DOI.10.1109/MNET.2005.1541715
  LABOVITZ2000: DOI.10.1145/347059.347428
  KUSHMAN2007: DOI.10.1145/1232919.1232927
  GRIFFIN1999: DOI.10.1145/316194.316231
  SAHOO2009: DOI.10.1016/j.comcom.2009.03.009
  LYCHEV2013: DOI.10.1145/2534169.2486010
  LI2014: DOI.10.14722/sent.2014.23001
  COOPER2013: DOI.10.1145/2535771.2535787
  ROTHENBERGER2017: DOI.10.1145/3065913.3065922
  MORILLO2021: DOI.10.14722/ndss.2021.24438
  KUMAR2007: DOI.10.1109/ICIMP.2007.42



--- abstract

The Internet has been successful beyond even the most optimistic expectations and is intertwined with many aspects of our society. Unfortunately, the security of today’s Internet is not commensurate with its importance as critical infrastructure. Additionally, the Internet has not primarily been built for high availability in the presence of malicious actors, and recent proposals to improve Internet security and availability have been constrained by the setup of the current architecture.

The next-generation inter-network architecture SCION (Scalability, Control, and Isolation On Next-generation networks) aims to address the above-mentioned issues. SCION was explicitly designed from the outset to offer availability and security by default. The architecture provides route control, failure isolation, and explicit trust information for end-to-end communication. It also enables multi-path routing between hosts.

This document gives a high-level overview of the SCION architecture, including its authentication model and the setup of the control- and data plane. As SCION is already in production use today, we conclude with an overview of SCION deployments.    


--- middle

# Introduction

The Introduction section explains why we designed SCION in the first place. It presents an overview of the Internet's most salient problems and shortcomings, which together are the reason why we developed SCION: To address these issues in order to make the Internet more secure, reliable, transparent, and efficient.

The sections after the Introduction provide further insight into SCION's main concepts and features. We complete the document with some concrete case studies where SCION has been applied successfully.


## Why SCION?

Two protocols effectively define today’s Internet architecture: the Internet Protocol (IP) {{RFC8200}}, {{RFC0791}} and the Border Gateway Protocol (BGP) {{RFC4271}}. These protocols have remained virtually unchanged since the standardization of IPv6 {{RFC2460}} and BGP-4 {{RFC1653}} in the 1990s. However, as the Internet continued to expand and needed to accommodate new uses, numerous issues came to light. The following sections describe these issues in more details.

### Internet Protocol

IP is one of the fundamental protocols of the Internet, as it enables the forwarding of packets between end hosts. Its first major version, IPv4, was specified in 1981 {{RFC0791}} and its (non-backward compatible) successor, IPv6, was introduced in 1998 {{RFC2460}}. After this, no major changes have taken place. The IP protocol follows a relatively simple approach: End hosts do not need to know the complete path to forward packets, nor can they influence the path the packets take. Unfortunately, this approach comes with many drawbacks:

- **Lack of transparency and control**  
Being able to select and verify the path that packets take is desirable in many situations. End hosts might want to avoid packets being routed through adversarial or untrusted networks, or they might want to choose the most suitable path with regard to a specific metric (e.g., latency or bandwidth). Unfortunately, IP does not offer such an option. Although systems that enable loose and strict source routing have been proposed, these extensions are not commonly supported in today’s networks. It is also not possible to simultaneously use multiple distinct paths towards the same destination.

- **Stateful routers**  
IP routers maintain forwarding tables to determine the next hop of a received packet. This basic requirement has undesirable consequences. Performing a forwarding-table lookup for every packet is a time-consuming operation. Therefore, high-performance networking equipment typically relies on ternary content-addressable memory (TCAM) hardware, which is expensive and energy-intensive. Moreover, the constantly growing size of forwarding tables, partially due to the slow but steady deployment of IPv6, poses a problem for routers, as the storage capacity of TCAM hardware is limited. Routers that keep state for network information can also suffer from denial-of-service (DoS) attacks exhausting the router’s state {{SCHUCHARD2011}}.

### BGP

BGP is the routing protocol that provides connectivity between autonomous systems (ASes), such as Internet service providers (ISPs). The protocol enables ISPs to perform traffic engineering and select routes based on policies that reflect the ISPs' business relationships. This happens through an intricate decision process that is used to select the best route to a destination {{CAESAR2005}}.
Unfortunately, BGP comes with a number of shortcomings:

- **Outages**    
Since the control plane and the data plane are not clearly separated in today’s Internet, forwarding may suddenly fail during route changes. By attacking routing, an adversary can thus interfere with packet forwarding. Furthermore, when BGP update messages are sent, the network may require up to tens of minutes to converge to a stable state {{LABOVITZ2000}}, which can lead to intermittent outages. As an indicator of these problems, a study has shown, for example, that a sudden degradation in user-perceived quality of voice-over-IP (VoIP) calls is highly correlated with BGP updates {{KUSHMAN2007}}.
- **Lack of fault isolation**   
BGP is a globally distributed protocol, running among all BGP speakers in the entire Internet. BGP update messages are thus disseminated globally. Due to the lack of any routing hierarchy or isolation between different areas, a single faulty BGP speaker can affect routing in the entire world.
- **Poor scalability**  
The amount of work required to be performed by BGP is proportional to the number of destinations. Moreover, path changes are disseminated profusely and sometimes throughout the entire Internet. This reduces scalability and prevents BGPsec from frequently disseminating freshly signed routing updates.
- **Convergence**  
ASes must have a consistent view of the network topology and agree on the set of paths to use for packet forwarding. Otherwise, AS A could configure AS B as the next hop for a particular destination, while B uses A as a next hop for the same destination. In this case, a packet would be sent back and forth between the two ASes, which constitutes a forwarding loop.
Unfortunately, convergence to a consistent and stable state depends on the policies of individual ASes. In certain situations, BGP will never converge to a stable state {{GRIFFIN1999}}. Other topologies cause BGP wedgies, where BGP converges but non-deterministically {{RFC4264}}. In general, BGP convergence after topology changes can require several minutes, during which users may experience outages {{SAHOO2009}}. In addition, BGP convergence constitutes an attack vector for malicious actors and makes verifying security and availability properties highly challenging.
- **Single path**  
BGP only allows the selection of a single path to a destination. Although some multipath protocols support simultaneous use of multiple network interfaces, BGP does not provide path control to end hosts and does not allow use of multiple AS-level paths. This can even lead to outages when BGP selects a legitimate but inefficient route through a link that is too small to satisfy the demand (bottleneck routing). In such a situation, end hosts have no choice but to wait until ASes in the Internet manually modify policies such that a more appropriate path is chosen.
- **Lack of security**  
BGP has no built-in security mechanisms and does not provide any tools for ASes to authenticate the information they receive through BGP update messages. This opens up a multitude of attack opportunities--see also [Attacks](#attack). RPKI and BGPsec tried to addressed these security issues in recent years. However, RPKI and BGPsec have problems of their own, as we discuss in the next section.

### RPKI and BGPsec

 Researchers recognized the issues arising from the lack of security mechanisms in core Internet protocols, and started working on improvements already in the late 1990s and early 2000s. While change was very slow initially (RPKI {{RFC6480}} and BGPsec {{RFC8205}} were only standardized in 2012 and 2017, respectively), there has been a substantial increase in RPKI deployment in recent years. However, RPKI and BGPsec have issues of their own, which we will discuss in the following sections. These issues made us believe that a more radical change to today’s Internet architecture will be necessary to fundamentally resolve its security problems.

#### RPKI and Route Origin Authorizations

RPKI provides certificates to ASes, and certificates for the IP addresses they own, which are called Route Origin Authorizations (ROAs). Unfortunately, ROAs only prevent the simplest form of BGP hijacks, see [Attacks](#attack).

#### Problems with BGPsec in Partial Deployment

BGPsec was standardized not before 2017, and it will likely take many years until it reaches global deployment. However, the protocol provides very little security benefits unless it is consistently used and enforced by all ASes, see {{LYCHEV2013}}. In a partial deployment, BGPsec can even cause instabilities and is prone to downgrade attacks.

#### Problems with BGPsec in Full Deployment

Even if all ASes in the world were to deploy BGPsec, many issues remain, such as the creation of wormholes and forwarding loops by attackers, or the introduction of circular dependencies, see {{LI2014}} and {{COOPER2013}}, respectively.  
RPKI and BGPsec also cause issues for network sovereignty {{ROTHENBERGER2017}}. As very few organizations are at the root of the RPKI hierarchy, these organizations have the power to create or revoke certificates. Depending on the jurisdiction, local courts of some countries may gain the power to shut down parts of the Internet, which makes some ISPs reluctant to deploy RPKI.  
Finally, BGPsec further exacerbates BGP’s scalability issues. To provide global connectivity, every one of the currently about 75,000 ASes in the world needs to know how to reach every other AS. This requires a large number of BGP update messages, the processing of which requires many more resources in BGPsec due to the additional cryptographic operations.  
Furthermore, prefix aggregation no longer works in BGPsec because the digital signatures are not aggregated. This is particularly cumbersome, as Internet routers need to store and exchange a fast-growing number of paths, caused by the increasing fragmentation of the IP address space and the trend towards announcing ever smaller IP address ranges.

### Lack of Authentication

Authenticating digital data is becoming increasingly important, as adversaries exploit the absence of authentication to inject malicious information. Infrastructures to provide authentication, such as RPKI/BGPsec, TLS {{RFC8446}}, and DNSSEC {{RFC4033}}, have been added in an ad-hoc manner.  
Unfortunately, all these protocols are sensitive to the compromise of a single entity. DNSSEC and RPKI rely on a single or very small number of roots of trust. TLS is based on an oligopolistic trust model, in which any one of hundreds of authorities can issue a certificate for any domain name. The Internet Control Message Protocol (ICMP) does not even have an authenticated counterpart, thus allowing the injection of fake ICMP packets, see {{RFC4443}} and {{RFC0791}}.  
The Internet neither supports the establishment of a shared secret key between two end hosts for encrypted and authenticated end-to-end communication; the simplest mechanism today is to rely on trust-on-first-use (TOFU) approaches. They opportunistically send the public key unauthenticated to the other communicating party.


### Attacks {#attack}

The current Internet architecture offers little to no protection against attacks such as prefix hijacking, spoofing, denial of service, DNS hijacking, and composed versions thereof (which use a combination
of vulnerabilities, or use a vulnerability in one protocol to compromise another protocol).

- **Prefix hijacking**  
Due to a lack of authentication and fault isolation in BGP, numerous Internet outages are caused by prefix hijacking, a malicious or erroneous announcement of IP address space. Prefix hijacking can also be used for interception (142). This problem is exacerbated by the fact that defining BGP routing policies is often a complicated, manual, and thus error-prone process.  
Unfortunately, BGP hijacks are still possible when RPKI is deployed and are only resolved in a full deployment of BGPsec: With RPKI, a malicious AS trying to hijack a particular IP prefix can still send a BGP update message claiming that it is directly connected to its legitimate owner (for which there exists a valid ROA). Recipients of such an announcement would accept it, since the legitimate owner of the addresses is noted as the last AS in the BGP message. They would then start sending traffic intended for those IP addresses to the attacker, who can inspect, reroute, or drop it.  
In settings where route origin validation (ROV) is deployed, Morillo et al. recently point out several new attacks: hidden hijack, non-routed prefix hijack, and super-prefix hijack of non-routed prefixes {{MORILLO2021}}.  
- **Spoofing and DDoS attacks**  
ICMP can be employed to send error or diagnostic messages (used by tools such as ping or traceroute). Because ICMP packets are not authenticated, the source address can easily be spoofed. This can lead to distributed denial-of-service (DDoS) attacks {{KUMAR2007}}, or be used to disconnect two BGP routers from each other {{RFC5927}}. Since regular IP packets are not authenticated either, they suffer from the same problem, i.e., the source IP address can be spoofed.


## Goals for a Secure Internet Architecture

Solutions should be/have:

- Available in the presence of adversaries
- Transparent and controllable
- Efficient and scalable
- Extensible and algorithm agile
- Deployable
- Formally verifiable


## Network Structure and Naming

SCION organizes existing ASes into groups of independent routing planes, called isolation domains (ISDs), which interconnect to provide global connectivity. Isolation domains provide natural isolation of routing failures and misconfigurations, give endpoints strong control over both inbound and outbound traffic, provide meaningful and enforceable trust, and enable scalable routing updates with high path-freshness.

As a path-based architecture, SCION end hosts learn about available network path segments, and combine them into end-to-end paths that are carried in packet headers. SCION also enables multi-path communication among end hosts.

SCION reuses the Autonomous Systems (AS) structure, and ensures that network traffic only flows on policy-compliant paths. To achieve scalability and sovereignty, Isolation Domains (ISD) are introduced. An ISD groups ASes that agree on a set of trust roots, called the Trust Root Configuration (TRC). An AS can be a member of multiple ISDs. The ISD is governed by a set of core ASes, which provide connectivity to other ISDs and manage the trust roots. Typically, the 3–10 largest ISPs of an ISD form the ISD’s core.

Routing is based on the <ISD, AS> tuple, agnostic of local addressing. Existing AS numbers are inherited from the current Internet, but a 48-bit namespace allows for additional SCION AS numbers beyond the 32-bit space in use today. Host addressing extends the network address with a local address, forming the <ISD, AS, local address> 3-tuple. The local address is not used in inter-domain routing or forwarding, does not need to be globally unique, and can thus be an IPv4, IPv6, or MAC address, for example.

## Conventions and Definitions

{::boilerplate bcp14-tagged}

# Key Concepts

## Authentication

Control-Plane PKI/TRC
From the book v2, use:  
chapter 2.2

## Control Plane

From the book v2, use:
chapters 2.1, 2.3, 2.5.

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

## Data Plane

From the book v2, use:
chapters 2.4, 5.1

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


# Deployments

SCI-ED, SSFC, SCIONLab
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

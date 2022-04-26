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
 -   ins: C. de Kater
     name: Corine de Kater
     org: ETH Zuerich
     email: corine.dekatermuehlhaeuser@inf.ethz.ch

 -   ins: A. Perrig
     name: Adrian Perrig
     org: ETH Zuerich
     email: adrian.perrig@inf.ethz.ch

normative:


informative:
  RFC4264:
  RFC0791:
  RFC4033:
  RFC4271:
  RFC4443:
  RFC6480:
  RFC8200:
  RFC8205:
  RFC8446:
  SCHUCHARD2011: DOI.10.1145/1866307.1866411
  LABOVITZ2000: DOI.10.1145/347059.347428
  GRIFFIN1999: DOI.10.1145/316194.316231
  SAHOO2009: DOI.10.1016/j.comcom.2009.03.009
  LYCHEV2013: DOI.10.1145/2534169.2486010
  LI2014: DOI.10.14722/sent.2014.23001
  COOPER2013: DOI.10.1145/2535771.2535787
  ROTHENBERGER2017: DOI.10.1145/3065913.3065922
  MORILLO2021: DOI.10.14722/ndss.2021.24438



--- abstract

The Internet has been successful beyond even the most optimistic expectations and is intertwined with many aspects of our society. Unfortunately, the security of today’s Internet is far from commensurate with its importance as critical infrastructure. Additionally, the Internet has not primarily been built for high availability in the presence of adversaries, and recent proposals to improve Internet security and availability have been constrained by the setup of the current architecture.

The next-generation inter-network architecture SCION (Scalability, Control, and Isolation On Next-generation networks) aims to address the above-mentioned issues. SCION was explicitly designed from the outset to offer availability and security by default. The architecture provides route control, failure isolation, and explicit trust information for end-to-end communication. It also enables multi-path routing between hosts.

This document discusses the motivations behind the SCION architecture and gives a high-level overview of its fundamental components, including its authentication model and the setup of the control- and data plane. As SCION is already in production use today, the document concludes with an overview of SCION deployments.


--- middle

# Introduction

The Internet has been incredibly successful as it grew to a planet-scale network with billions of devices. But although this world-wide communication system guarantees global reachability, it falls short of providing other properties that are in demand today. These shortcomings of the current Internet are the reason for developing SCION: To make the Internet more secure, reliable, transparent, and scalable.

The Introduction section further explores the motivation to develop SCION, followed by a short description of SCION's main elements. The sections after the Introduction provide deeper insight into SCION's key concepts and features. The document concludes with some concrete case studies where SCION has been applied successfully.


## Why SCION - Motivation  {#why}

Since its introduction back in the 1980s (1970s?), the Internet has never stopped to expand. As a consequence, the global network continually needs to accommodate new uses. This has brought many issues to light. To name the most important: a lack of transparency and control, poor scalability, occurrences of severe outages, weak fault isolation, and (stateful) routing that becomes increasingly time- and energy-consuming. As the Internet has not been built with security in mind, the lack thereof is another major issue. The implementation of authentication leaves room for improvement, too. Because of this, the current Internet offers little protection against attacks such as spoofing, prefix- and DNS-hijacking, denial-of-service, and combinations of them.       

Up until now, there have been numerous initiatives to address the above issues (see rfcs rpki, bgpsec). Although these initiatives have brought many improvements, concerns regarding security and scalability still remain (see ). Also other requirements that users have of today's Internet, such as high availability and performance, end-host path selection, as well as multi-path communication, are not fulfilled yet (see among others draft-king-irtf-challenges-in-routing-08).

SCION has been developed in order to bridge these gaps. SCION improves: availability in the presence of adversaries, offers path control and transparency, is efficiency and scalability, trustworthiness, security, extensibility, and easy deployment.
SCION improves ....
--> add more see paper Cyrill.




### Challenges with IP routing

Today's IP routing suffers from significant limitations that are a result of original design decisions. The Internet has never stopped to expand and continually needs to accommodate new use cases that were not originally taken into account. This has brought numerous issues to light, listed in the following sections.

#### Internet Protocol

IP comes with the following drawbacks:

- **Lack of programmable paths**
IP addressing is tightly coupled with routing, therefore packets follow the path established by the routing protocol. End hosts are not able to select paths based on application requirements or path conditions. In addition, it is also not possible to simultaneously use multiple distinct paths towards the same destination.
- **Lack of security and transparency**
IP end hosts are oblivious to the path taken by their packets. This means that end hosts have no visibility nor guarantees on where their traffic is forwarded. This may cause traffic to be redirected through adversary points, breaching the payload's security.
- **Scalability**
The use of forwarding tables in IP routers is time-consuming, expensive, and energy-intensive. Also, the constantly growing size of forwarding tables causes storage problems. Additionally, routers that keep state for network information can suffer from denial-of-service (DoS) attacks exhausting the router’s state {{SCHUCHARD2011}}.

#### BGP

Just as IP, also BGP suffers from a number of shortcomings:

- **Convergence time in case of outages**
The distributed nature of BGP control plane results in convergence times up to ten minutes or more {{LABOVITZ2000}}, resulting in slow failover and intermittent transient connectivity.
- **Lack of fault isolation**
Due to the lack of any routing hierarchy or isolation between different areas, a single faulty BGP speaker can affect routing in the entire world.
- **Poor scalability**
As the number of connected devices grows, so does the number of prefixes, posing additional strain on the protocol. Scalability challenges are particularly evident when considering  BGPSec {{RFC8205}}.
- **Convergence**
BGP convergence can be problematic, too. In certain situations, BGP will never converge to a stable state, or converge only non-deterministically (see {{GRIFFIN1999}} and {{RFC4264}}. Convergence may also take too much time {{SAHOO2009}}.
- **Single path**
BGP only allows the selection of a single path to a destination. But having a multi-path choice can be welcome in several situations, e.g., in the case of a link failure, for load balancing, or when traffic is routed based on different policies.
- **Lack of security**
BGP has no built-in security mechanisms and does not provide any tools for ASes to authenticate the information they receive through BGP update messages. This opens up a multitude of attack opportunities--see [Attacks](#attack).

### Issues with RPKI and BGPsec

 RPKI and BGPsec try to address Internet's above-mentioned security shortcomings, see also {{RFC6480}} and {{RFC8205}}. However, RPKI and BGPsec introduce additional challenges, as shortly described below.

- **RPKI and Route Origin Authorizations**
Unfortunately, the Route Origin Authorizations (ROAs) provided by RPKI only prevent the simplest form of BGP hijacks, see [Attacks](#attack).
- **Problems with BGPsec in partial deployment**
BGPsec only provides full security when all ASes consistently use and enforce it. In case of partial deployment, it has a limited effectiveness. It can even cause instabilities and is prone to downgrade attacks, see {{LYCHEV2013}}.
- **Problems with BGPsec in full deployment**
Also full deployment of BGPsec raises issues, such as the creation of wormholes and forwarding loops by attackers, or the introduction of circular dependencies, see {{LI2014}} and {{COOPER2013}}. RPKI and BGPsec together also cause issues for network sovereignty {{ROTHENBERGER2017}}.
- **Scalability** BGPsec further exacerbates BGP’s scalability issues (i.e., due to the additional overhead, and due to lack of prefix aggregation). Lack of scalable implementations represent still today a large obstacle to adoption.

### Other Internet Issues

#### Lack of Authentication

Authenticating digital data is becoming increasingly prevalent, as adversaries exploit the absence of authentication to inject malicious information. Specifically, many network protocols do not use authentication at all, leaving them exposed to multiple attacks:

- Today's Internet lacks a fundamental mechanism to share a secret key between two end hosts for secure end-to-end communication. Existing approaches (i.e., SSH) resort to trust-on-first-use (TOFU) approach, where an host's initial public key is accepted without verification.
- Infrastructures were added over time to provide authentication, such as RPKI/BGPsec, TLS {{RFC8446}}, and DNSSEC {{RFC4033}}. However, they  are all sensitive to the compromise of a single entity.
- The Internet Control Message Protocol (ICMP) lacks an authenticated counterpart, see {{RFC4443}} and {{RFC0791}}. Unauthenticated ICMP messages can potentially be used to affect or even prevent traffic forwarding. TODO: complete


#### Attacks {#attack}

The current Internet architecture offers little to no protection against several attacks, such as prefix hijacking, spoofing, denial of service, DNS hijacking, and composed versions thereof. Unfortunately, BGP hijacks are still possible when RPKI is deployed and are only resolved in a full deployment of BGPsec. Additionally, in settings where route origin validation (ROV) is deployed, Morillo et al. recently point out several new attacks: hidden hijack, non-routed prefix hijack, and super-prefix hijack of non-routed prefixes {{MORILLO2021}}.


## SCION Overview

SCION has been designed to address the security issues of today's Internet depicted in the previous section [Why SCION - Motivation](#why). This section gives a high-level description of SCION's main elements, providing a basic understanding of this next-generation inter-network architecture.

### Network Architecture and Naming

SCION's main goal is to offer highly available and efficient inter-domain packet delivery—even in the presence of actively malicious entities. To achieve scalability and sovereignty, SCION organizes existing ASes into groups of independent routing planes, called **Isolation Domains (ISD)**. An AS can be a member of multiple ISDs. All ASes in an ISD agree on a set of trust roots, called the **Trust Root Configuration (TRC)**, ensuring that network traffic only flows on policy-compliant paths. The ISD is governed by a set of **core ASes**, which provide connectivity to other ISDs and manage the trust roots. Typically, the 3–10 largest ASes of an ISD form the ISD’s core.

Isolation domains serve the following purposes:

- They allow SCION to support trust heterogeneity, as each ISD can independently define its roots of trust;
- They provide transparency for trust relationships;
- They isolate the routing process within an ISD from external influences such as attacks and misconfigurations; and
- They improve the scalability of the routing protocol by separating it into a process within and one between ISDs.

ISDs provide natural isolation of routing failures and misconfigurations, give endpoints strong control over both inbound and outbound traffic, provide meaningful and enforceable trust, and enable scalable routing updates with high path-freshness.

**Links**
There are three types of links in SCION: core links, parent-child links, and peering links.

- A **core link** can only exist between two core ASes.
- A **parent-child link** requires that at least one of the two connected ASes is a non-core AS. ASes with a parent-child link usually belong to the same entity or have a provider-customer relationship.
- A **peering link** also includes at least non-core AS. A peering link exists between ASes with a (standard or paid) relationship.

Figure 1 shows a high-level overview of the SCION network structure:

figure: !(SCIONnetwork)

                                  Figure 1: SCION network structure

|
|
o  Parent AS - child AS    ----  Peering link    ===  Core link


### Routing

SCION operates on two routing levels: intra-ISD and inter-ISD. As a path-based architecture, SCION end hosts learn about available network path segments through **path-segment construction beacons (PCBs)**. A PCB is initiated by a core AS and then disseminated either within an ISD (to explore intra-ISD paths) or among core ASes (to explore core paths across different ISDs). The PCBs accumulate cryptographically protected path- and forwarding information on AS-level, and store this information in the form of **hop fields (HFs)**. End hosts use the information from these PCBs/hop fields to create end-to-end forwarding paths for data packets, who carry this information in their packet headers. This concept is called **packet-carried forwarding state (PCFS)**. The concept also supports multi-path communication among end hosts.

The process of creating an end-to-end forwarding path consists of the following steps:

1. First, an AS discovers paths to other ASes, during the *path exploration* (or beaconing) phase.
2. The AS then selects a few PCBs according to defined policies, transforms the selected PCBs into path segments, and registers these segments with a path infrastructure, thus making them available to other ASes. This happens during the *path registration* phase.
3. During the *path resolution* phase, the actual creation of an end-to-end forwarding path to the destination takes place. For this, an end host performs
      a. a *path lookup* step, to obtain path segments, and
      b. a *path combination* step, to combine the forwarding path from the segments.

**ISD and AS numbering**
SCION decouples end-host addressing from inter-domain routing. Routing is based on the <ISD, AS> tuple, agnostic of end-host addressing. Existing AS numbers are inherited from the current Internet, but a 48-bit namespace allows for additional SCION AS numbers beyond the 32-bit space in use today. The end host local address is not used for inter-domain routing or forwarding, does not need to be globally unique, and can thus be an IPv4, IPv6, or MAC address, for example. A SCION address is therefore composed of the <ISD, AS, local address> 3-tuple.

### Infrastructure Components

The **beacon service**, the **path service**, and the **certificate service** are the main infrastructure components within a SCION AS. Each service can be deployed redundantly, depending on the AS's size and type. It is also possible to combine the services into one or more *control services*. *Internal routers* forward packets inside the AS, while *border routers* provide interconnectivity between ASes.

- The beacon service discovers path information. It is responsible for generating, receiving, and propagating PCBs. Periodically, the beacon service generates a set of PCBs, which are forwarded to its child ASes or neighboring core ASes. The PCBs are flooded over policy-compliant paths to discover multiple paths between any pair of core ASes.
- The path service stores mappings from AS identifiers to sets of announced path segments. The path service is organized as a hierarchical caching system similar to that of DNS. Through the beacon service, ASes select the set of path segments through which they want to be reached, and they register them to the path service in the ISD core.
- The certificate service keeps cached copies of certificates and manages keys and certificates for securing inter-AS communication. The certificate service is queried by the beacon service when validating the authenticity of PCBs (i.e., when the beacon service lacks a certificate).

*Border routers* are deployed at the edge of SCION ASes. The main task of border routers is to forward packets to a neighbor border router or the destination host within the AS. While SCION takes care of intra-domain routing, it relies on existing routing protocols (e.g., IS-IS, OSPF, SDN) and communication fabric (e.g., IP, MPLS) for intra-domain forwarding.  *Internal routers*, therefore, do not need to be changed to support SCION.



## Conventions and Definitions

{::boilerplate bcp14-tagged}

# Key Concepts


## Authentication

SCION’s control plane relies on a public-key infrastructure we call the **control-plane PKI (CP-PKI)**, in which each ISD defines its own roots of trust and policies in a file called trust root configuration (TRC). A TRC is a signed collection of certificates, which also contains ISD-specific policies, for example, specifying how many signatures an updated TRC should contain to be valid.
Each SCION AS must hold a private key (to sign PCBs) and a certificate attesting that it is the rightful owner of the corresponding public key. One of the main roles of the TRC is thus enabling the verification of **AS certificates** and PCBs.

## Control Plane

The SCION control plane discovers and distributes AS-level path segments. A path segment encodes a network path at the granularity
of inter-domain interfaces on either end of an inter-domain link connecting two consecutive ASes on a path.
<!-- Constructing inter-domain paths at the granularity of inter-AS links increases the number of available paths and enables optimization of paths with regard to different criteria. -->

Each end-to-end path consists of up to three path segments: core path, up-path, and down-path segments. Core-path segments
refer to path segments containing only core ASes, an up-path segment is a path segment from a customer (leaf AS) to a provider
(core AS) inside one ISD, and a down-path segment is a path segment from a provider (core AS) to a customer (leaf AS) inside
an ISD.

To address the sub-optimality of hierarchical routing, SCION introduces peering links and shortcuts. In a shortcut, a path only contains an up-path and a down-path segment, which can cross over at a non-core AS that is common to both paths. Peering links can be added to up- or down-path segments, resulting in an operation similar to today’s Internet.

Routing (or path segment construction) is conducted hierarchically on two levels: (1) among all core ASes of all ISDs, which constructs core-path segments, and (2) within each ISD, which constructs up- and down-path segments. The path segment construction process is referred to as beaconing, where a Path-segment Construction Beacon (PCB) is initiated by core ASes to iteratively construct path segments. Up- and down-path segments are interchangeable, simply by reversing the order of ASes in a segment. The beaconing process in each AS is performed by its beacon server which is a part of its Control Service (CS), that performs control-plane-related tasks.

Core beaconing is the process of constructing path segments between core ASes. During core beaconing, a core AS either initiates PCBs or propagates PCBs received from neighboring core ASes to all other neighboring core ASes.

Intra-ISD beaconing is the second level of the beaconing hierarchy, which creates path segments from core ASes to non-core ASes. For this, core ASes create PCBs and send them to their non-core neighbors (typically customer ASes). Each non-core AS propagates the received PCBs to its respective customers. This procedure continues until the PCB reaches an AS without any customer (leaf AS) and as a result, all ASes receive path segments to reach the core ASes of their ISD. Non-core ASes can include their peering links in the PCBs, enabling valley-free forwarding if both up- and down-path segments contain the same peering link.

A global path server infrastructure is used to disseminate path segments. Each AS contains a path server as a part of the control service. The infrastructure bears similarities to DNS, where information is fetched on-demand only. A core AS’s path server stores all the intra-ISD path segments that were registered by leaf ASes of its own ISD, and core-path segments to reach other core ASes.

## Data Plane

Name resolution in SCION returns the <ISD, AS, local address> 3-tuple. Core- and down-path segments are fetched based on the <ISD, AS> tuple. Hosts can then combine one of their up-path segments with the received core- and down-path segments.

Shortcut paths that avoid a core AS are possible, if the up- and down-path contain the same AS, or if a peering link is available between an AS in the up-path and an AS in the down-path segment. Cryptographic protections ensure authentic path segments and prevent unauthorized path combinations.

The path segments contain compact hop-fields, that encode information about which interfaces may be used to enter and leave an AS. The hop-fields are cryptographically protected, preventing path alteration. This so-called Packet-Carried Forwarding State (PCFS) replaces signaling to use a path, ensuring that routers do not need any local state on either paths or flows.


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

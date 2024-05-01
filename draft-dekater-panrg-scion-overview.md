---
title: "SCION Overview"
abbrev: "SCION I-D"
category: info
submissiontype: IRTF

docname: draft-dekater-panrg-scion-overview-latest
v: 3
area: IRTF
workgroup: PANRG
keyword: Internet-Draft
venue:
  group: WG
  type: Working Group
  mail: panrg@irtf.org
  arch: https://datatracker.ietf.org/rg/panrg
  github: scionassociation/scion-overview_I-D
  latest: https://scionassociation.github.io/scion-overview_I-D/draft-dekater-panrg-scion-overview.html

author:
 -   ins: C. de Kater
     name: Corine de Kater
     org: SCION Association
     email: cdk@scion.org

 -   ins: N. Rustignoli
     name: Nicola Rustignoli
     org: SCION Association
     email: nic@scion.org

 -   ins: A. Perrig
     name: Adrian Perrig
     org: ETH Zuerich
     email: adrian.perrig@inf.ethz.ch

normative:
  RFC5280:


informative:
  RFC1918:
  RFC4264:
  RFC4033:
  RFC5218:
  RFC6480:
  RFC8205:
  RFC8446:
  RFC9049:
  RFC9217:
  RFC8170:
  RFC8200:
  SCHUCHARD2011: DOI.10.1145/1866307.1866411
  LABOVITZ2000: DOI.10.1145/347059.347428
  GRIFFIN1999: DOI.10.1145/316194.316231
  SAHOO2009: DOI.10.1016/j.comcom.2009.03.009
  LYCHEV2013: DOI.10.1145/2534169.2486010
  LI2014: DOI.10.14722/sent.2014.23001
  COOPER2013: DOI.10.1145/2535771.2535787
  ROTHENBERGER2017: DOI.10.1145/3065913.3065922
  MORILLO2021: DOI.10.14722/ndss.2021.24438
  KLENZE2021: DOI.10.1109/CSF51468.2021.00018
  DERUITER2021: DOI.10.1145/3485983.3494839
  ANDERSEN2001: DOI.10.1145/502034.502048
  KATZ2012: DOI.10.1145/2377677.2377756
  KUSHMAN2007: DOI.10.1145/1232919.1232927
  PERRIG2017:
    title: "SCION: A Secure Internet Architecture"
    date: 2017
    target: https://doi.org/10.1007/978-3-319-67080-5
    seriesinfo:
      ISBN: 978-3-319-67079-9
    author:
      -
        ins: A. Perrig
        name: Adrian Perrig
        org: ETH Zuerich
      -
        ins: P. Szalachowski
        name: Pawel Szalachowski
        org: ETH Zuerich
      -
        ins: R. Reischuk
        name: Raphael Reischuk
        org: ETH Zuerich
      -
        ins: L. Chuat
        name: Laurent Chuat
        org: ETH Zuerich
  KING2022:
    title: Challenges for the Internet Routing Systems Introduced by Semantic Routing
    date: 2022
    target: https://datatracker.ietf.org/doc/draft-king-irtf-challenges-in-routing/
    author:
      -
        ins: D. King
        name: Daniel King
        org: Lancaster University
      -
        ins: A. Farrel
        name: Adrian Farrel
        org: Old Dog consulting
      -
        ins: C. Jacquenet
        name: Christian Jacquenet
        org: Orange
  HITZ2021:
    title: Demonstrating the reliability and resilience of Secure Swiss Finance Network
    date: 2021
    target: https://perma.cc/4H3Q-WZNG
    author:
      ins: S. Hitz
      name: Samuel Hitz
      org: Anapaya Systems
  LEGNER2020:
     title: "EPIC: Every Packet Is Checked in the Data Plane of a Path-Aware Internet"
     date: 2020
     target: https://www.usenix.org/conference/usenixsecurity20/presentation/legner
     author:
       -
         ins: M. Legner
         name: Adrian Perrig
         org: ETH Zuerich
       -
         ins: T. Klenze
         name: Tobias Klenze
         org: ETH Zuerich
       -
         ins: M. Wyss
         name: Marc Wyss
         org: ETH Zuerich
       -
         ins: C. Sprenger
         name: Christoph Sprenger
         org: ETH Zuerich
       -
         ins: A. Perrig
         name: Adrian Perrig
         org: ETH Zuerich
  CHUAT22:
    title: "The Complete Guide to SCION"
    date: 2022
    target: https://doi.org/10.1007/978-3-031-05288-0
    seriesinfo:
      ISBN: 978-3-031-05287-3
    author:
      -
        ins: L. Chuat
        name: Laurent Chuat
        org: ETH Zuerich
      -
        ins: M. Legner
        name: Markus Legner
        org: ETH Zuerich
      -
        ins: D. Basin
        name: David Basin
        org: ETH Zuerich
      -
        ins: D. Hausheer
        name: David Hausheer
        org: Otto von Guericke University Magdeburg
      -
        ins: S. Hitz
        name: Samuel Hitz
        org: Anapaya Systems
      -
        ins: P. Mueller
        name: Peter Mueller
        org: ETH Zuerich
      -
        ins: A. Perrig
        name: Adrian Perrig
        org: ETH Zuerich

  I-D.rustignoli-scion-components:
    title: SCION Components Analysis
    date: 2023
    target: https://datatracker.ietf.org/doc/draft-rustignoli-panrg-scion-components/
    author:
      -
        ins: C. de Kater
        name: Corine de Kater
        org: SCION Association
      -
        ins: N. Rustignoli
        name: Nicola Rustignoli
        org: SCION Association

  I-D.dekater-scion-pki:
    title: SCION Control-Plane PKI
    date: 2023
    target: https://datatracker.ietf.org/doc/draft-dekater-scion-pki/
    author:
      -
        ins: C. de Kater
        name: Corine de Kater
        org: SCION Association
      -
        ins: N. Rustignoli
        name: Nicola Rustignoli
        org: SCION Association

  I-D.dekater-scion-controlplane:
    title: SCION Control Plane
    date: 2023
    target: https://datatracker.ietf.org/doc/draft-dekater-scion-controlplane/
    author:
      -
        ins: C. de Kater
        name: Corine de Kater
        org: SCION Association
      -
        ins: M. Frei
        name: Matthias Frei
        org: SCION Association
      -
        ins: N. Rustignoli
        name: Nicola Rustignoli
        org: SCION Association

  I-D.dekater-scion-dataplane:
    title: SCION Data Plane
    date: 2023
    target: https://datatracker.ietf.org/doc/draft-dekater-scion-dataplane/
    author:
      -
        ins: C. de Kater
        name: Corine de Kater
        org: SCION Association
      -
        ins: N. Rustignoli
        name: Nicola Rustignoli
        org: SCION Association


--- abstract

The Internet has been successful beyond even the most optimistic expectations and is intertwined with many aspects of our society. But although the world-wide communication system guarantees global reachability, the Internet has not primarily been built with security and high availability in mind. The next-generation inter-network architecture SCION (Scalability, Control, and Isolation On Next-generation networks) aims to address these issues. SCION was explicitly designed from the outset to offer security and availability by default. The architecture provides route control, failure isolation, and trust information for end-to-end communication. It also enables multi-path routing between hosts.

This document discusses the motivations behind the SCION architecture and gives a high-level overview of its fundamental components, including its authentication model and the setup of the control- and data plane. As SCION is already in production use today, the document concludes with an overview of SCION deployments.

For detailed descriptions of SCION's components, refer to {{I-D.dekater-scion-pki}}, {{I-D.dekater-scion-controlplane}}, and {{I-D.dekater-scion-dataplane}}. A more detailed analysis of relationships and dependencies between components is available in {{I-D.rustignoli-scion-components}}.

--- middle

# Introduction

The Introduction section explores the motivation to develop SCION, followed by a short description of SCION's main elements. The sections after the Introduction provide further insight into SCION's key concepts and deployment scenarios. The document concludes with some concrete case studies where SCION has been successfully deployed in production.

## Terminology {#terms}

**MAC**: Message Authentication Code. In the rest of this document, "MAC" always refers to "Message Authentication Code" and never to "Medium Access Control". When "Medium Access Control address" is implied, the phrase "Link Layer Address" is used.

## Why SCION - Motivation {#why}

Since its inception, the Internet has continued to expand, encompassing new uses over time. The continuous expansion has brought many issues to light, including a lack of control, limitations in scalability, performance and security, occurrences of severe outages, weak fault isolation, and energy consumption. With the core focus on functionality and operation, the current Internet offers little protection against attacks such as spoofing, IP-address hijacking, denial-of-service, and combinations of these. For more background information, see {{SCHUCHARD2011}}, {{LABOVITZ2000}}, {{GRIFFIN1999}}, {{SAHOO2009}}, and {{RFC4264}}.

There have been numerous initiatives to address the above issues. Although these initiatives have brought many improvements, concerns regarding security and scalability still remain. For more details, see, e.g., {{RFC4033}}, {{RFC6480}}, {{RFC8205}}, and {{RFC8446}}, as well as {{LYCHEV2013}}, {{LI2014}}, {{COOPER2013}}, {{ROTHENBERGER2017}}, {{MORILLO2021}}, and {{KING2022}}.

As a consequence, today's Internet fails to fulfil many users' requirements. This especially pertains to the demands of enterprises globally exchanging sensitive information, such as financial institutions, healthcare providers, universities, multinationals, governments, critical and transportation infrastructure operators. These users require the Internet to be highly available at all times. They expect reliable operation of the global network also in case of failures. They need availability guarantees across multiple routing domains, even in the presence of attacks. They further want to rely on an Internet that can be multilaterally governed and is free from global kill-switches.

SCION has been developed in order to meet the above-mentioned requirements. SCION aims to reach the following goals:

- Provide high-availability architecture (also in the presence of adversaries)
- Provide fast failover in the case of inter-domain link or router failures
- Prevent from IP-address hijacking, DoS, and other attacks
- Enable path transparency as well as application-specific path optimizations
- Improve the inter-domain control plane's scalability
- Prepare the Internet for tomorrow's applications, such as virtual reality, Internet of Things (IoT), and all other applications requiring high-performance connectivity.


### Scope of SCION

The above section describes SCION's aspiration to improve *inter*-AS routing and to focus on providing end-to-end connectivity. However, SCION does not solve *intra*-AS routing issues, nor does it provide end-to-end payload encryption, and identity authentication. These topics, which are equally important for the Internet to perform well, lie outside the scope of SCION.

### Practical Considerations Based on Related RFCs

The SCION inter-domain routing concept has initially been developed by researchers of the ETH Zuerich {{PERRIG2017}}, and could in the meantime also gain attention and recognition in the international academic world. However, for an IT architecture to be successful, it must work well in practice, too. This section pays attention to the implementation considerations of a conceptual framework such as SCION in real life, on the basis of some RFCs exploring this topic. It also verifies in how far SCION meets the requirements mentioned and questions raised in these RFCs.

#### Avoiding Pitfalls

{{RFC9049}} describes why previous proposals to tackle some of the Internet's fundamental issues did not manage to succeed. SCION seems to avoid the pitfalls mentioned in that document. For example, SCION does not have to be adopted by the entire Internet to be effective: The routing architecture provides benefits already to early adapters. Even if only a small part of the global network works with SCION, adapters will still take advantage of using the SCION routing technology. Moreover, not only users of SCION benefit from it, also ISPs and operators benefit from deploying SCION: early deployments showed that providers can charge the use of SCION as premium connectivity, with users who are willing to pay for it. Furthermore, SCION can be installed on top of and function alongside the existing routing infrastructure and protocols--there is no need for high-impact changes in an operational network.

Another RFC that must be mentioned in this context is {{RFC5218}}, "What Makes for a Successful Protocol?". SCION seems to fulfil most factors that contribute to the success of a protocol, as described in section 2.1 of the RFC. This includes such factors as offering a positive net value (i.e., the benefits of deploying SCION outweigh the costs), incremental deployability, and open source code availability. More importantly, SCION averts the failure criteria mentioned in section 1.4 of the RFC: SCION is already deployed and in use by many actors of the Swiss financial and academic ecosystems, and allows for multiple implementations, both open and closed source. As existing SCION implementations are easily portable, adoption in mainstream platforms is also possible.

#### Answering Questions

SCION can be considered a _path-aware internetworking_ architecture, as described in {{RFC9217}}. This RFC poses (open) questions that must be answered in order to realize such a path-aware networking system. It was originally written to frame discussions in the Path Aware Networking Research Group (PANRG), and has been published to snapshot current thinking in this space.

SCION intends to answer the questions raised in this RFC. This especially pertains to the second, third, seventh, and eighth question:

- How do endpoints and applications get access to accurate, useful, and trustworthy path properties?
- How can endpoints select paths to use for traffic in a way that can be trusted by the network, the endpoints, and the applications using them?
- How can a path-aware network in a path-aware internetwork be effectively operated, given control inputs from network administrators, application designers, and end users?
- How can the incentives of network operators and end users be aligned to realize the vision of path-aware networking, and how can the transition from current ("path-oblivious") to path-aware networking be managed?

SCION's answers to these questions can be found in [Key Concepts](#key) and [Deployments](#deploy), respectively.

### Why Now?

The emergence of multiple SCION implementations and early deployments highlights the need for standardization. The time seems therefore ripe to take SCION to the IETF, also in order to contribute to the important discussion regarding path-aware networking.

## SCION Overview

SCION has been designed to address the fundamental issues of today's Internet depicted in [Why SCION - Motivation](#why). The following section gives a high-level overview of SCION's main elements, providing a basic understanding of this next-generation inter-network architecture.

### Network Architecture and Naming

SCION's main goal is to offer highly available and efficient inter-domain packet delivery—even in the presence of actively malicious entities. To achieve scalability and sovereignty, SCION organizes existing ASes into groups of independent routing planes, called **Isolation Domains (ISD)**. An AS can be a member of multiple ISDs. All ASes in an ISD agree on a set of trust roots, called the **Trust Root Configuration (TRC)**. The ISD is governed by a set of **core ASes**, which provide connectivity to other ISDs and manage the trust roots. Typically, a few distinguished ASes within an ISD form the ISD’s core.

Isolation domains serve the following purposes:

- They allow SCION to support trust heterogeneity, as each ISD can independently define its roots of trust;
- They provide transparency for trust relationships;
- They isolate the routing process within an ISD from external influences such as attacks and misconfigurations; and
- They improve the scalability of the routing protocol by separating it into a process within and one between ISDs.

ISDs provide natural isolation of routing failures and misconfigurations, provide meaningful and enforceable trust, enable endpoints to optionally restrict traffic forwarding to trusted parts of the Internet infrastructure only, and enable scalable routing updates with high path-freshness.


#### Links

Within and between ISDs, SCION supports three types of links: (1) core links, (2) parent-child links, and (3) peering links.

- A **core link** always connects two core ASes, which are either within the same or in a different ISD. Core links can exist for various underlying business relationships, including provider-customer (where the customer pays the provider for traffic) and peering relationships.
- A **parent-child link** creates a hierarchy between the parent and the child. ASes with a parent-child link typically have a provider-customer relationship.
- **Peering links** exist between ASes with a (settlement-free or paid) peering relationship. Peering links can only be used to reach destinations within or downstream of the peering AS. They can be established between any two core or non-core ASes, and between core and non-core ASes. Peering links can also cross ISD boundaries.

See {{architecture}} for a high-level overview of the SCION network structure.

~~~~
+-------------------------------------+
|                                     |
| +-[TRC]---------------------------+ |  +----------------------------+
| |       ISD Core                  | |  | +-[TRC]------------------+ |
| |                                 | |  | |            ISD Core    | |
| | .---.        .---.       .---.  | |  | | .---.        .---.     | |
| |(CAS A)*----*(CAS B)*---*(CAS C)*--------*CAS I)*----*(CAS J)    | |
| | `-#-'        `-#-'       `-#-'  | |  | | `-#-'        `-#-'     | |
| |   |            |           |    | |  | |   |            |       | |
| |   |            |           |    | |  | |   |            |       | |
| |   |            |           |    | |  | |   |            |       | |
| +---|------------|-----------|----+ |  | +---|------------+-------+ |
|     |            |           |      |  |     |            |         |
|   .-0-.          |         .-0-.    |  |   .-0-.        .-0-.       |
|  (AS D )         |    +---# AS E)   |  |  (AS K )< - ->( AS L)      |
|   `-#-'          |    |    `-#-'    |  |   `-#-'        `---'       |
|     |            |    |      |      |  |     |                      |
|     |            |    |      |      |  |     |                      |
|     |            |    |      |      |  |     |           ISD 2      |
|     |            |    |      |      |  |     |                      |
|     |            |    |      |      |  |     |                      |
|   .-0-.        .-0-0--+    .-0-.    |  |   .-0-.                    |
|  (AS F )< - ->( AS G)     (AS H )< -|- - >(AS M )                   |
|   `---'        `---'       `---'    |  |   `---'                    |
|                                     |  +----------------------------+
|                                     |
|   ISD 1                             |
|                                     |
+-------------------------------------+

 parent-child link #-------0    CAS: core AS
         core link *-------*    TRC: trust root configuration
      peering link < - - - >
~~~~
{: #architecture title="SCION network structure"}


### Routing

SCION provides path-aware inter-domain routing between ASes across the Internet. The SCION control plane is responsible for discovering these inter-domain paths and making them available to the endpoints within the ASes. SCION inter-domain routing operates on two levels: Within a SCION isolation domain (ISD), which is called *intra*-ISD routing, and between ISDs, called *inter*-ISD routing. Both levels use the so-called *path-segment construction beacons (PCBs)* to explore network paths. A PCB is initiated by a core AS and then disseminated either within an ISD to explore intra-ISD paths, or among core ASes, to explore core paths across different ISDs.

The PCBs accumulate cryptographically protected path and forwarding information on AS-level, and store this information in the form of *hop fields*. Endpoints use information from these hop fields to create end-to-end forwarding paths for data packets, who carry this information in their packet headers. This concept is called *packet-carried forwarding state*. The concept also supports multi-path communication among endpoints.

The creation of an end-to-end forwarding path consists of the following processes:

- *Path exploration (or beaconing)*: This is the process where an AS discovers paths to other ASes.
- *Path registration*: This is the process where an AS selects a few PCBs, according to defined policies, turns the selected PCBs into path segments, and adds these path segments to the relevant path infrastructure, thus making them available to other ASes.
- *Path resolution*: This is the process of actually creating an end-to-end forwarding path from the source endpoint to the destination. For this, an endpoint performs (a) a path lookup step, to obtain path segments, and (b) a path combination step, to combine the forwarding path from the segments. This last step takes place in the data plane.

All processes operate concurrently.

For detailed information on path exploration, registration, and lookup, see {{I-D.dekater-scion-controlplane}}. For a detailed description of the path combination and construction process, see {{I-D.dekater-scion-dataplane}}.

{{beaconing}} below shows the SCION routing processes and their relation to each other.

~~~~
+-------------------------+       +-------------------------+
| Exploration (Beaconing) |------>|      Registration       |
+-------------------------+       +-----------+-------------+
                                              |
                              +---------------+
                              |
     +------------------------v------------------------+
     |                 Path Resolution                 |
     |                                                 |
     |   +----------------+       +----------------+   |
     |   |     Lookup     +------>|  Combination   |   |
     |   |                |       |    (Data Plane)|   |
     |   +----------------+       +----------------+   |
     +-------------------------------------------------+
~~~~
{: #beaconing title="SCION routing processes and their relation to each other. All processes operate concurrently."}


#### Path Segments

As described previously, the main goal of SCION's control plane is to create and manage path segments, which can then be combined into forwarding paths to transmit packets in the data plane. SCION distinguishes the following types of path segments:

- A path segment from a non-core AS to a core AS is an **up-segment**.
- A path segment from a core AS to a non-core AS is a **down-segment**.
- A path segment between core ASes is a **core-segment**.

Each path segment either ends at a core AS, or starts at a core AS, or both.

**Note**: There are no SCION path segments that start and end at a non-core AS. However, when combining path segments into an end-to-end SCION path, it is possible to use peering links.

All path segments are invertible: A core-segment can be used bidirectionally, and an up-segment can be converted into a down-segment, or vice versa, depending on the direction of the end-to-end path. This means that all path segments can be used to send data traffic in both directions.


#### ISD and AS numbering

The inter-domain SCION routing is based on the <ISD, AS> tuple. Although a complete SCION address is composed of the <ISD, AS, endpoint address> 3-tuple, the endpoint address is not used for inter-domain routing or forwarding. The endpoint address can be of variable length, does not need to be globally unique, and can thus be an IPv4, IPv6, or link layer address, for example - in fact, the endpoint address is the "normal", currently used, non-SCION-specific endpoint address.

**Note**: As a consequence of the fact that SCION relies on existing routing protocols (e.g., IS-IS, OSPF, SR) and communication fabric (e.g., IP, MPLS) for intra-domain forwarding, existing internal routers do not need to be changed to support SCION.


#### Control Service {#infra-components}

The **control service** is responsible for the path exploration and registration processes in the control plane. It is the main control-plane infrastructure component within each SCION AS. The control service of an AS has the following tasks:

- Generating, receiving, and propagating PCBs. Periodically, the control service of a core AS generates a set of PCBs, which are forwarded to the child ASes or neighboring core ASes. In the latter case, the PCBs are sent over policy-compliant paths to discover multiple paths between any pair of core ASes.
- Selecting and registering the set of path segments via which the AS wants to be reached.
- Managing certificates and keys to secure inter-AS communication. Each PCB contains signatures of all on-path ASes. Every time the control service of an AS receives a PCB, it validates the PCB's authenticity. When the control service lacks an intermediate certificate, it can query the control service of the neighboring AS that sent the PCB.

**Note:** The control service of an AS must not be confused with a border router. The control service of a specific AS is part of the control plane and responsible for *finding and registering suitable paths*. It can be deployed anywhere inside the AS. A border router belongs to the data plane; its main task is to *forward data packets*. Border routers are deployed at the edge of an AS.


### Link Failures

Unlike in the current Internet, link failures are not automatically resolved by the network, but require active handling by endpoints. Since SCION forwarding paths are static, they break when one of the links fails. Link failures are handled by a two-pronged approach that typically masks link failures without any outage to the application and rapidly re-establishes fresh working paths:

- The SCION Control Message Protocol (SCMP) (the SCION equivalent of ICMP) is used for signaling connectivity problems. Instead of relying on application- or transport-layer timeouts, endpoints get immediate feedback from the network if a path stops working, and can quickly switch to an alternative path.
- SCION endpoints are encouraged to use multipath communication by default, thus masking a link failure with another working path. As multipath communication can increase availability (even in environments with very limited path choices), the SCION control services attempt to create, select and announce disjoint paths, and endpoints compose path segments to achieve maximum resilience to path failure. Consequently, most link failures in SCION remain unnoticed by the application, unlike the frequent (albeit mostly brief) outages in the current Internet. See also {{ANDERSEN2001}}, {{KATZ2012}}, {{KUSHMAN2007}}, and {{HITZ2021}}.


### Formal Verification

An additional feature of SCION is its formal verification. The SCION network system consists of a variety of components such as routers, servers, and edge devices. Such a complex system eludes the mental capacities of human beings for considering all possible states and interactions. That is why SCION includes a formal verification framework developed by the Department of Computer Science of the ETH Zurich {{KLENZE2021}}. This guarantees that packet forwarding as well as SCION's authentication mechanisms and implementations are correct and consistent.


## Conventions and Definitions

{::boilerplate bcp14-tagged}


# Key Concepts {#key}

This section explains the SCION key concepts, including authentication, control- and data plane.

## The Control-Plane PKI

SCION's control plane relies on a public-key infrastructure called the **control-plane PKI (CP-PKI)**, which is organized on ISD-level. Each ISD can independently build its own roots of trust, defined in a file called **trust root configuration (TRC)**.

**Note**: This document describes the SCION control-plane PKI on a very high level. For a detailed specification of the SCION control-plane PKI, see {{I-D.dekater-scion-pki}}.

### Control-Plane PKI - Overview

Authentication in SCION is based on digital certificates that bind identifiers to public keys and carry digital signatures that are verified by roots of trust. SCION allows each ISD to define its own set of trust roots, along with the policy governing their use. Such scoping of trust roots within an ISD improves security, as compromise of a private key associated with a trust root cannot be used to forge a certificate outside the ISD. An ISD's trust roots and policy are encoded in the TRC, which has a version number, a list of public keys that serves as root of trust for various purposes, and policies governing the number of signatures required for performing different types of actions. The TRC serves as a way to bootstrap all authentication within SCION. Additionally, TRC versioning is used to efficiently revoke compromised roots of trust.

Each TRC consists of a collection of signed root certificates, which are used to sign CA certificates, which are in turn used to sign AS certificates. The TRC also includes ISD-policies that specify, for example, the TRC's usage, validity, and future updates. A TRC is a fundamental component of an ISD's control-plane PKI. The so-called **base TRC** constitutes the ISD's trust anchor and is thus axiomatically trusted. It is signed during a signing ceremony by so-called voting ASes and then distributed throughout the ISD. All ASes within an ISD must be pre-loaded with the currently valid base TRC of their own ISD.

### Overview of Certificates, Keys, and Roles

All certificates used in SCION's control-plane PKI are in X.509 v3 format {{RFC5280}}. Additionally, the TRC contains self-signed certificates instead of plain public keys. Self-signed certificates have the following advantages over plain public keys: (1) They make the binding between name and public key explicit; and (2) the binding is signed to prove possession of the corresponding private key.

All ASes in SCION have the task to sign and verify control-plane messages. However, certain ASes have additional roles:

- **Core ASes**: Core ASes are a distinct set of ASes in the SCION control plane. For each ISD, the core ASes are listed in the TRC. Each core AS in an ISD has links to other core ASes (in the same or in different ISDs).
- **Certification authorities (CAs)**: CAs are responsible for issuing AS certificates to other ASes and/or themselves.
- **Voting ASes**: Only certain ASes within an ISD may sign TRC updates. The process of appending a signature to a new TRC is called "casting a vote"; the designated ASes that hold the private keys to sign a TRC update are "voting ASes".
- **Authoritative ASes**: Authoritative ASes are those ASes in an ISD that always have the latest TRCs of the ISD. They start the announcement of a TRC update.


### TRC Updates

There are two types of TRC updates: regular and sensitive. A *regular* TRC update is a periodic re-issuance of the TRC where the entities and policies listed in the TRC remain unchanged, whereas a *sensitive* TRC update is an update that modifies critical aspects of the TRC, such as the set of core ASes. In both cases, the base TRC remains unchanged. If the ISD's TRC has been compromised, it is necessary for an ISD to re-establish the trust root. This is possible with a process called trust reset (if allowed by the ISD's trust policy). In this case, a new base TRC is created. For more details on a trust reset, see {{reset}}.

{{chain}} shows the TRC trust chain and associated certificates. TRC 1 is the base TRC, and TRC 2 and 3 constitute updates to this base TRC. TRC 2 must be verified using the voting certificates in TRC 1. Control-plane (CP) root certificates are used to verify other CP certificates (which are in turn used to verify path-segment construction beacons PCBs).

~~~~
                               TRC 2
               +--------------------------------------+
               |+------------------------------------+|
               ||- Version       - Core ASes         ||
+--------+     ||- ID            - Description       ||    +--------+
| TRC 1  |     ||- Validity      - No Trust Reset    ||    | TRC 3  |
| (Base  |---->||- Grace Period  - Voting Quorum     ||--->|        |
|  TRC)  |     ||- ...                               ||    |        |
+--------+     |+------------------------------------+|    +--------+
               |+----------------+  +----------------+|
               || Regular Voting |  |Sensitive Voting||
               ||  Certificate   |  |  Certificate   ||
               |+----------------+  +----------------+|
               |+----------------+  +----------------+|
               ||     Votes      |  |   Signatures   ||
               |+----------------+  +----------------+|
               |+------------------------------------+|
               ||        CP Root Certificates        ||
               |+----------+-------------+-----------+|
               |           |             |            |
               +-----------+-------------+------------+
                           |             |
                           |             |
                           v             v
                 +-----------+         +-----------+
                 |   CP CA   |         |   CP CA   |
                 |Certificate|         |Certificate|
                 +-+-------+-+         +-----+-----+
                   |       |                 |
                   |       |                 |
                   v       v                 v
          +-----------+ +-----------+      +-----------+
          |   CP AS   | |   CP AS   |      |   CP AS   |
          |Certificate| |Certificate|      |Certificate|
          +-----------+ +-----------+      +-----------+
~~~~
{: #chain title="Chain of trust within an ISD"}


#### Discovering TRC Updates

SCION provides the following mechanisms for discovering TRC updates:

- *Beaconing Process*: The TRC version is announced in the beaconing process. Each AS must announce what it considers to be the latest TRC. Furthermore, each AS must include the hash value of the TRC contents to facilitate the discovery of discrepancies. Therefore, relying parties that are part of the beaconing process discover TRC updates passively: A core AS notices TRC updates for remote ISDs that are on the beaconing path. A non-core AS only notices TRC updates for the local ISD through the beaconing process, if it receives a PCB with a TRC version number higher than the locally stored TRC. The creation of a new TRC should trigger the generation of new control-plane messages, as the propagation of control-plane messages will help other ASes rapidly discover the new TRC. This simple dissemination mechanism has two advantages: (1) It is very efficient (as fresh PCBs rapidly reach all ASes), and (2) it avoids circular dependencies with regard to the verification of PCBs and the beaconing process itself (as no server needs to be contacted over unknown paths in order to fetch the updated TRC).
- *Path Lookup*: In every path segment, all ASes must reference the latest TRC of their ISD. Therefore, when resolving paths, every relying party will notice TRC updates, even remote ones. Note that this mechanism only works when there is an active communication between the relying party and the ISD in question.


### Revocation and Recovery from a Catastrophic Event {#reset}

The TRC dissemination mechanism also enables rapid revocation of trust roots. When a trust root is compromised, the other trust roots can remove it from the TRC and disseminate a new TRC alongside a PCB with a new version number.

In case of a catastrophic event—such as several private root keys being disclosed due to a critical vulnerability in a cryptographic library—SCION is equipped with a recovery procedure called **trust reset**. This procedure consists of creating a new TRC with fresh, trustworthy keys (and potentially new algorithms), and redistributing this TRC out-of-band. A trust reset effectively establishes a new base TRC for the ISD. It is possible for ISDs to disable trust resets by setting the _no trust reset_ Boolean parameter to "true" in their TRC, with the effect that the entire ISD would have to be abandoned in the event of such a catastrophic compromise (this abandonment would also have to be announced out-of-band).

The partition of the SCION network into ISDs guarantees that no single entity can take down the entire network. Even if several entities formed a coalition to carry out an attack, the effects of that attack would be limited to one or a few ISDs.


## SCION Control Plane

The SCION control plane is responsible for discovering path segments and making them available to endpoints.

**Note**: This section describes the SCION control plane on a very high level. For a detailed specification of the SCION control plane, see {{I-D.dekater-scion-controlplane}}.


### Path Exploration

Path exploration is the process where an AS discovers paths to other ASes. In SCION, this process is referred to as **beaconing**. This section gives a high level explanation of the SCION beaconing process.

In SCION, the *control service* of each AS is responsible for the beaconing process. The control service generates, receives, and propagates so-called **path-segment construction beacons (PCBs)** on a regular basis, to iteratively construct path segments. PCBs contain topology and authentication information, and can also include additional metadata that helps with path management and selection. The beaconing process itself is divided into routing processes on two levels, where *inter*-ISD or core beaconing is based on the (selective) sending of PCBs without a defined direction, and *intra*-ISD beaconing on top-to-bottom propagation.

- *Inter-ISD or core beaconing* is the process of constructing path segments between core ASes in the same or in different ISDs. During core beaconing, the control service of a core AS either initiates PCBs or propagates PCBs received from neighboring core ASes to other neighboring core ASes. Core beaconing is periodic; PCBs are sent over policy-compliant paths to discover multiple paths between any pair of core ASes.
- *Intra-ISD beaconing* creates path segments from core ASes to non-core ASes. For this, the control service of a core AS creates PCBs and sends them to the non-core child ASes (typically customer ASes). The control service of a non-core child AS receives these PCBs and forwards them to its child ASes, and so on. This procedure continues until the PCB reaches an AS without any customer (leaf AS). As a result, all ASes within an ISD receive path segments to reach the core ASes of their ISD.

On its way, a PCB accumulates cryptographically protected path- and forwarding information per traversed AS. At every AS, metadata as well as information about the AS's ingress and egress interfaces (i.e., link identifiers) are added to the PCB. The ingress and egress interface IDs identify connections to neighboring ASes. These IDs only need to be unique within each AS. Therefore, they can be chosen and encoded by each AS independently and without any need for coordination.

SCION also supports shortcuts and peering links. In a *shortcut*, a path only contains an up-path and a down-path segment, which can cross over at a non-core AS that is common to both paths. *Peering links* can be added to up- or down-path segments, resulting in an operation similar to today’s Internet.

Note that PCBs do not traverse peering links. Instead, peering links are announced along with a regular path in a PCB. If both ASes at either end of a peering link have registered path segments that include this specific peering link, then it is possible to use this peering link during segment combination to create the end-to-end path.


#### Selection of PCBs to Propagate

As an AS receives a series of intra-ISD or core PCBs, it must select the PCBs it will use to continue beaconing. Each AS can independently set policies dictating which PCBs are propagated in which time intervals, and to which neighbors. The selection process can be based on path properties (e.g., length, disjointness across different paths) as well as on PCB properties (e.g., age, remaining lifetime of sent instances) - each AS is free to use those properties that suit the AS best. The control service can then compute the overall quality of each candidate PCB based on these properties. For this, the AS should use a selection algorithm or metric that reflects its needs and requirements and identifies the best PCBs or paths segments for this AS.

For a detailed description of selecting PCBs to propagate, see the section "Selection of PCBs to Propagate" in {{I-D.dekater-scion-controlplane}}.



#### Propagating a PCB

Every propagation period (as configured by the AS), the control service

- selects the best combinations of PCBs and interfaces connecting to a neighboring AS (i.e., a child AS or a core AS), and
- sends each selected PCB to the selected egress interface(s) associated with it.

For every selected PCB and egress interface combination, the AS extends the PCB by adding a so-called *AS entry* to the selected PCB. Such an AS entry includes a hop field that specifies the incoming (ingress) and outgoing (egress) interface for the packet forwarding through this AS, in the beaconing direction. The AS entry can also contain peer entries.

For a detailed description of the propagation of a PCB, see the sections "PCB Propagation - Illustrated Example" and "Propagation of Selected PCBs" in {{I-D.dekater-scion-controlplane}}.


### Path Registration

Path registration is the process where an AS transforms selected PCBs into path segments, and adds these segments to the relevant path databases, thus making them available to other ASes.

As mentioned previously, a non-core AS typically receives several PCBs representing several path segments to the core ASes of the ISD the AS belongs to. Out of these PCBs, the non-core AS selects those down-path segments through which it wants to be reached, based on AS-specific selection criteria. The next step is to register the selected down-segments with the control service of the relevant core ASes, according to a process called *intra-ISD path-segment registration*. As a result, a core AS's control service contains all intra-ISD path segments registered by the non-core ASes of its ISD. In addition, each core AS control service also stores preferred core-path segments to other core ASes, in the *core-segment registration* process.

For a detailed description of path-segment registration, see the section "Registration of Path Segments" in {{I-D.dekater-scion-controlplane}}.


#### Intra-ISD Path-Segment Registration

Every *registration period* (determined by each AS), the AS's control service selects two sets of PCBs to transform into two types of path segments:

- Up-segments, which allow the infrastructure entities and endpoints in this AS to communicate with core ASes; and
- down-segments, which allow remote entities to reach this AS.

The up- and down-segments do not have to be equal.  An AS may want to communicate with core ASes via one or more up-segments that differ from the down-segment(s) through which it wants to be reached. Therefore, an AS can define different selection policies for the up- and down-segment sets.


#### Core Path-Segment Registration

The core beaconing process creates path segments from core AS to core AS. These core-segments are then added to the control service path database of the core AS that created the segment, so that local and remote endpoints can obtain and use these core-segments. In contrast to the intra-ISD registration procedure, there is no need to register core-segments with other core ASes (as each core AS will receive PCBs originated from every other core AS).


### Path Lookup

The *path lookup* is a fundamental building block of SCION's path management, as it enables endpoints to obtain path segments found during path exploration and registered during path registration. This allows the endpoints to construct end-to-end paths from the set of possible path segments returned by the path lookup process. The lookup of paths still happens in the control plane, whereas the construction of the actual end-to-end paths happens in the data plane.


#### Lookup Process

An endpoint (source) that wants to start communication with another endpoint (destination), requires up to three path segments:

- An up-path segment to reach the core of the source ISD (only if the source endpoint is a non-core AS),
- a core-path segment to reach

  - another core AS in the source ISD, in case the destination AS is in the same source ISD, or
  - a core AS in a remote ISD, if the destination AS is in another ISD, and

- a down-path segment to reach the destination AS.

**Note**: The actual number of required path segments depends on the location of the destination AS as well as on the availability of shortcuts and peering links. More information on combining and constructing paths is provided by the {{I-D.dekater-scion-dataplane}} document.

The process to look up and fetch path segments consists of the following steps:

1. First, the source endpoint queries the control service in its own AS (i.e., the source AS) for the required segments. The control service has up-path segments stored in its path database. Additionally, the control service checks if it has appropriate core- and down-path segments in store as well; in this case it returns them immediately.
2. If there are no appropriate core-segments and down-segments, the control service in the source AS queries the control services of the reachable core ASes in the source ISD, for core-path segments to core ASes in the destination ISD (which is either the own or a remote ISD). To reach the core control services, the control service of the source AS uses the locally stored up-path segments.
3. Next, the control service of the source AS combines up-path segments with the newly retrieved core-path segments. The control service then queries the control services of the remote core ASes in the destination ISD, to fetch down-path segments to the destination AS. To reach the remote core ASes, the control service of the source AS uses the previously obtained and combined up- and core segments.
4. Finally, the control service of the source AS returns all retrieved path segments to the source endpoint.
5. Once it has obtained all path segments, the endpoint combines them into an end-to-end path in the data plane.


#### Caching

For the sake of efficiency, the control service of the source AS should cache each returned path segment request. Caching ensures that path lookups are fast for frequently used destinations. The use of caching is also essential to ensure that the path-lookup process is scalable and can be performed with low latency. Additionally, it is good practice to send requests in parallel when requesting path segments from other control services.



## SCION Data Plane

While the control plane is responsible for providing end-to-end paths, the data plane ensures that packets are forwarded on the selected path. The SCION data plane fundamentally differs from today's IP-based data plane in that it is *path-aware*: In SCION, inter-domain forwarding directives are embedded in the packet header.

SCION routers are deployed at the edge of an AS, and peer with neighbor SCION routers. Inter-domain forwarding is based on end-to-end path information contained in the packet header. This path information consists of a sequence of hop fields. Each hop field corresponds to an AS on the path, and it includes an ingress- as well as an egress interface ID, which univocally identify the ingress and egress interfaces within the AS. The information is authenticated with a Message Authentication Code (MAC) to prevent forgery. This concept allows SCION routers to forward packets to a neighbor AS without inspecting the destination address and also without consulting an inter-domain forwarding table; the SCION router can just access the next hop from the packet header.

*Intra*-domain forwarding and routing are based on existing mechanisms (e.g., IP). A SCION border router reuses existing intra-domain infrastructure to communicate to other SCION routers or SCION endpoints within its AS. The last SCION router at the destination AS therefore uses the destination address to forward the packet to the appropriate local endpoint.

The SCION design choice has the following advantages:

- It provides control and transparency over forwarding paths to endpoints.
- It simplifies the packet-processing at routers: Instead of having to perform longest-prefix matching on IP addresses, which requires expensive hardware and substantial amounts of energy, a router can simply access the next hop from the packet header, after having verified the authenticity of the hop field's MAC.

**Note**: This section describes the SCION data plane on a very high level. A much more detailed description of SCION's data plane is available in {{I-D.dekater-scion-dataplane}}.


### Path Construction via Segment Combination

Paths are discovered by the SCION control plane, which makes them available to SCION endpoints in the form of path segments. There are three kinds of path segments: up, down, and core. In the data plane, a SCION endpoint creates end-to-end paths from the path segments, by combining multiple path segments. Depending on the network topology, a SCION forwarding path can consist of one, two, or three segments. Each path segment contains several hop fields representing the ASes on the segment as well as one info field with basic information about the segment, such as a timestamp.

{{combinations}} below shows the different allowed segment combinations.

**Note**: It is assumed that the source and destination endpoints are in different ASes.


~~~~
                                  ------- = end-to-end path
   C = Core AS                    - - - - = unused links
   * = source/destination AS      ------> = direction of beaconing


          Core                        Core                  Core
      ---------->                 ---------->           ---------->
     .-.       .-.               .-.       .-.         .-.       .-.
+-- ( C )-----( C ) --+     +-- ( C )-----(C/*)       (C/*)-----(C/*)
|    `+'       `+'    |     |    `+'       `-'         `-'       `-'
|     |    1a   |     |     |     |     1b                   1c
|     |         |     |     |     |
|     |         |     |     |     |
|    .+.       .+.    |     |    .+.                       Core
|   (   )     (   )   |     |   (   )                 -------------->
|    `+'       `+'    |     |    `+'                        .-.
|     |         |     |     |     |                   +----( C )----+
|     |         |     |     |     |                   |     `-'     |
|     |         |     |     |     |                   |             |
|    .+.       .+.    |     |    .+.                 .+.     1d    .+.
+-> ( * )     ( * ) <-+     +-> ( * )               (C/*)         (C/*)
     `-'       `-'               `-'                 `-'           `-'



          .-.                      .-.                   .-.
+--   +--( C )--+   --+      +--  (C/*)        +--    - ( C ) -    --+
|     |   `-'   |     |      |     `+'         |     |   `-'   |     |
|     |         |     |      |      |          |                     |
|     |    2a   |     |      |  2b  |          |     |    3a   |     |
|     |         |     |      |      |          |                     |
|    .+.       .+.    |      |     .+.         |    .+.       .+.    |
|   (   )     (   )   |      |    (   )        |   (   #-----#   )   |
|    `+'       `+'    |      |     `+'         |    `+'  Peer `+'    |
|     |         |     |      |      |          |     |         |     |
|     |         |     |      |      |          |     |         |     |
|     |         |     |      |      |          |     |         |     |
|    .+.       .+.    |      |     .+.         |    .+.       .+.    |
+-> ( * )     ( * ) <-+      +->  ( * )        +-> ( * )     ( * ) <-+
     `-'       `-'                 `-'              `-'       `-'


          Core                                    Core
      ---------->                              ---------->
     .-.       .-.             .-.            .-.       .-.        .-.
 +--( C )- - -( C )--+  +---- ( C ) ----+    ( C )- - -( C )  +-- ( C )
 |   `+'       `+'   |  |      `+'      |     `+'       `+'   |    `+'
 |         3b        |  |           4a  |          4b         |  5
 |    |         |    |  |       |       |      |         |    |     |
 |                   |  |               |                     |
 |   .+.       .+.   |  |      .+.      |      + - --. - +    |    .+.
 |  (   #-----#   )  |  |   +-(   )-+   |      +--(   )--+    |   ( * )
 |   `+'  Peer `+'   |  |   |  `-'  |   |      |   `-'   |    |    `+'
 |    |         |    |  |   |       |   |      |         |    |     |
 |    |         |    |  |   |       |   |      |         |    |     |
 |    |         |    |  |   |       |   |      |         |    |     |
 |   .+.       .+.   |  |  .+.     .+.  |     .+.       .+.   |    .+.
 +->( * )     ( * )<-+  +>( * )   ( * )<+    ( * )     ( * )  +-> ( * )
     `-'       `-'         `-'     `-'        `-'       `-'        `-'
~~~~
{: #combinations title="Illustration of possible path-segment combinations. Each node represents a SCION Autonomous System."}


The following path-segment combinations are allowed:

- *Communication through core ASes*:

  - *Core-segment combination* (Cases 1a, 1b, 1c, 1d in {{combinations}}): The up- and down-segments of source and destination do not have an AS in common. In this case, a core-segment is required to connect the source's up- and the destination's down-segment (Case 1a). If either the source or the destination AS is a core AS (Case 1b) or both are core ASes (Cases 1c and 1d), then no up- or down-segment(s) are required to connect the respective AS(es) to the core-segment.
  - *Immediate combination* (Cases 2a, 2b in {{combinations}}): The last AS on the up-segment (which is necessarily a core AS) is the same as the first AS on the down-segment. In this case, a simple combination of up- and down-segments creates a valid forwarding path. In Case 2b, only one segment is required.

- *Peering shortcut* (Cases 3a and 3b): A peering link exists between the up- and down-segment. The extraneous path segments to the core are cut off. Note that the up- and down-segments do not need to originate from the same core AS and the peering link could also be traversing to a different ISD.
- *AS shortcut* (Cases 4a and 4b): The up- and down-segments intersect at a non-core AS below the ISD core, thus creating a shortcut. In this case, a shorter path is made possible by removing the extraneous part of the path to the core. Note that the up- and down-segments do not need to originate from the same core AS and can even be in different ISDs (if the AS at the intersection is part of multiple ISDs).
- *On-path* (Case 5): In the case where the source's up-segment contains the destination AS or the destination's down-segment contains the source AS, a single segment is sufficient to construct a forwarding path. Again, no core AS is on the final path.

Once a forwarding path is chosen, it is encoded in the SCION packet header, making inter-domain routing tables unnecessary for the SCION routers. The destination can respond to the source by reversing the end-to-end path from the packet header, or it can perform its own path lookup and combination.


### SCION Header Specification

As mentioned above, when a source endpoint wants to communicate with a destination endpoint in SCION, it encodes the end-to-end path made up out of path segments in the SCION packet header. This section introduces the SCION header structure and specification. A much more detailed description of the SCION header is provided in the section "SCION Header Specification" of the SCION Data Plane draft {{I-D.dekater-scion-dataplane}}.


#### SCION Packet Header

The SCION packet header is composed of a common header, an address header, a path header, and an optional extension header:

~~~~
+--------------------------------------------------------+
|                     Common header                      |
|                                                        |
+--------------------------------------------------------+
|                     Address header                     |
|                                                        |
+--------------------------------------------------------+
|                      Path header                       |
|                                                        |
+--------------------------------------------------------+
|              Extension header (optional)               |
|                                                        |
+--------------------------------------------------------+
~~~~
{: #header title="High-level SCION header structure"}

- The **common header** contains important meta information like a version number and the lengths of the header and payload. In particular, it contains flags that control the format of subsequent headers such as the address and path headers.
- The **address header** contains the ISD-, AS-, and endpoint-addresses of source and destination.
- The **path header** contains the full AS-level forwarding path of the packet. The `PathType` field in the common header specifies the path format used in the path header.
- Finally, the optional **extension header** contains a variable number of hop-by-hop and end-to-end options, similar to the extensions in the IPv6 header {{RFC8200}}.

This document continues with a high-level description of the SCION path header. For a detailed description of the SCION path header, and of the other SCION headers (common-, address-, and extension header), see the SCION Data Plane draft {{I-D.dekater-scion-dataplane}}.


#### Path Header

The `SCION` path type is the standard SCION path type. The path header for the `SCION` path type consists of a path meta header, up to 3 info fields and up to 64 hop fields. It has the following layout:

~~~~
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                          PathMetaHdr                          |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                           InfoField                           |
|                                                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                              ...                              |
|                                                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                           InfoField                           |
|                                                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                           HopField                            |
|                                                               |
|                                                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                           HopField                            |
|                                                               |
|                                                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                              ...                              |
|                                                               |
|                                                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
~~~~
{: #scion-path-header title="Layout of a standard SCION path header"}


- The Path Meta Header (`PathMetaHdr`) indicates the currently valid info field and hop field while the packet is traversing the network along the path, as well as the number of hop fields per path segment.
- The number of info fields (`InfoField`) equals the number of path segments that the path contains - there is one info field per path segment. Each info field contains basic information about the corresponding segment, such as a timestamp indicating the creation time. There are also two flags. One specifies whether the path segment must be traversed in construction (beaconing) direction, the other whether the first or last hop field in the path segment represents a peering hop field.
- Each hop field (`HopField`) represents a hop through an AS on the path, with the ingress and egress interface identifiers for this AS. This information is authenticated with a Message Authentication Code (MAC) to prevent forgery.

The SCION path header is created by extracting the required info fields and hop fields from the corresponding path segments, which were looked up by the source endpoint in the control plane.

A detailed description of the path header and its creation is provided in the section "Path Header" of the SCION Data Plane draft {{I-D.dekater-scion-dataplane}}.


### Path Authorization

It is crucial for the data plane that endpoints only use paths constructed and authorized by ASes in the control plane. In particular, endpoints should not be able to craft hop fields themselves, modify hop fields in authorized path segments, or combine hop fields of different path segments (path splicing). The property that prevents this is called **path authorization** (see {{KLENZE2021}} and {{LEGNER2020}}).

SCION uses cryptographic mechanisms to efficiently provide path authorization. The mechanisms are based on *symmetric* cryptography in the form of message-authentication codes (MACs) in the data plane to secure forwarding information encoded in hop fields. Each AS calculates these MACs using a local secret key (that is only shared between SCION infrastructure elements within the AS) and chains them to the previous hop fields on the path. The MACs are then included in the forwarding path as part of the respective hop fields.

Detailed information on path authorization in the SCION data plane is provided in the section "Path Authorization" of the SCION Data Plane draft {{I-D.dekater-scion-dataplane}}.


### Intra-AS Communication

As SCION is an *inter*-domain network architecture, it is not concerned with *intra*-domain forwarding. This corresponds to the general practice today where BGP and IP are used for inter-domain routing and forwarding, respectively, but ASes use an intra-domain protocol of their choice, for example OSPF or IS-IS for routing and IP, MPLS, and various layer-2 protocols for forwarding.

SCION emphasizes this separation, as SCION is used exclusively for inter-domain forwarding, and re-uses the intra-domain network fabric to provide connectivity among all SCION infrastructure services, border routers, and endpoints. As a consequence, minimal change to the infrastructure is required for ISPs when deploying SCION.

Although a complete SCION address is composed of the <ISD, AS, endpoint address> 3-tuple, the endpoint address is not used for inter-domain routing or forwarding. This implies that the endpoint addresses are not required to be globally unique or globally routable, they can be selected independently by the corresponding ASes. This means, for example, that an endpoint identified by a link-local IPv6 address in the source AS can directly communicate with an endpoint identified by a globally routable IPv4 address via SCION. Alternatively, it is possible for two SCION hosts with the   same IPv4 address 10.0.0.42 but located in different ASes to communicate with each other via SCION ({{RFC1918}}).



# Deployment

Adoption of a next-generation architecture is a challenging task, as it needs to be integrated with, and operate alongside existing infrastructure. SCION is designed to coexist with existing intra-domain routing infrastructure, and comprises coexistence and transition mechanisms that facilitate adoption, in accordance to principles defined in {{RFC8170}}.
The following section discusses practical considerations for deploying SCION and briefly touches on some of the transition mechanisms, with focus on:

* [Autonomous Systems](#deployment-as),

* [Internet Exchange Points](#deployment-ixp), and

* [endpoints](#deployment-end-host), covering both native SCION hosts and SCION to IP encapsulation.

We then describe some of the early adopters deployment experiences. A more detailed adoption plan is to be outlined in dedicated documents.

## Autonomous System Deployment {#deployment-as}

A SCION AS needs to deploy the SCION [infrastructure components](#infra-components) and border routers.
Within an AS, SCION is often deployed as an IP overlay on top of the existing network. This way SCION allows to reuse the existing intra-domain network and equipment (e.g., IP, MPLS). Customer-side SCION border routers directly connect to the provider-side border routers using last-mile connections. The SCION design assumes that AS’s internal entities are considered to be trustworthy, therefore the IP overlay or the first-hop routing does not compromise or degrade any security properties SCION delivers.
When it comes to inter-domain communication, an overlay deployment on top of today’s Internet is not desirable, as SCION would inherit issues from  its weak underlay. Thus, inter-AS SCION links are usually deployed in parallel to existing links, in order to preserve its security properties. That is, two SCION border routers from neighbour ASes are directly connected via a layer-2 cross-connection at a common point-of-presence.

 All SCION AS components can be deployed on standard x86 commercial off-the-shelf servers or virtual machines. In fact, SCION border routers do not rely on forwarding tables, therefore they do not require specialized hardware. Practice shows that off-the-shelf hardware can handle up to 100 Gbps links, while a prototype [P4 implementation](#DERUITER2021) showed that it is possible to forward SCION traffic even at terabit speeds.

 Overall, an AS can be connected to SCION without high-impact changes to its network. In addition, use of commodity hardware for both control and data-plane components reduces initial deployment costs.


## Internet Exchange Points {#deployment-ixp}

Internet Exchange Points (IXP) play as important a role for SCION as they do in today's Internet.  SCION can be deployed at existing IXPs following a "big switch" model, where the IXP provides a large L2 switch between multiple SCION ASes. SCION has been deployed following this model at the Swiss Internet Exchange (SwissIX),  currently interconnecting major SCION Swiss ISPs and enterprises through bi-lateral peering over dedicated SCION ports.

Additionally, thanks to its path-awareness, SCION offers the option of an enhanced deployment model, i.e., to expose the internal topology of an IXP within the SCION control plane. This enables IXP customers to use SCION’s multipath and fast failover capabilities to leverage the IXP’s internal links (including backup links) and to select paths depending on the application’s needs.  IXPs have therefore an incentive to expose their rich internal connectivity, as the benefits from SCION’s multipath capabilities would increase their value for customers and provide them with a competitive advantage.

## Endpoints and Incremental Deployability {#deployment-end-host}

End users can leverage SCION in two different ways: (1) using SCION-aware applications on a [SCION native endpoint](#native-endhost), or (2) using transparent [IP-to-SCION conversion](#sig). The benefit of using SCION natively is that the full range of advantages becomes available to applications, at the cost of installing the SCION endpoint stack and making the application SCION-aware. In early deployments, the second approach is often preferred, so that no changes are needed within applications or endpoints.



### Native Endpoints {#native-endhost}
A SCION native endpoint's stack consists of a dispatcher, which handles all incoming and outgoing SCION packets, and of a SCION daemon, which handles control-plane messages. The latter  fetches paths to remote ASes and provides an API for applications and libraries to interact with the SCION control plane (i.e., for path lookup, SCION extensions). The current SCION implementation uses an UDP/IP underlay for communication between endpoints and SCION routers. This allows reuse of existing intra-domain networking infrastructure. SCION endpoints can optionally use automated bootstrapping mechanisms to retrieve configuration from the network and establish SCION connectivity. This way, clients require no pre-existing network-specific configurations.

### SCION to IP Gateway (SIG) {#sig}
A SCION-IP-Gateway (SIG) encapsulates regular IP packets into SCION packets with a corresponding SIG at the destination that performs the decapsulation.
A SIG can be deployed close to the end user (i.e., at branches of an enterprise, on a CPE), or within an ISP's network. In the latter case, the SIG is called carrier-grade SIG, as it serves multiple customers within the AS where it is deployed. This approach has the advantage that it does not require any changes at the customer's premises.
In order to allow incremental deployability and to ease transition from legacy IP-based Internet to SCION, SIGs can be augmented with  mechanisms allowing them to coordinate and automatically exchange IP prefix information. A more detailed description of the SIG and its coordination mechanisms is to be presented in dedicated documents.

## Deployment Experiences {#deploy}

SCION has been deployed in production by multiple entities, growing its acceptance among industry. While early deployments started on academic and research networks, SCION has expanded to serve the financial industry, government, and it is being evaluated for the healthcare sector.

In 2017, SCION was evaluated for production use by a central bank, with the goal of modernising the network interconnecting banks and their branches. SCION was chosen, as it allows moving away from a dedicated private network to a reliable Internet-based solution. SCION connectivity was later extended to support system-critical applications, like the national real-time gross settlement (RTGS) system, connecting all country's banks to exchange real-time payment information.
The network, called Secure Swiss Finance Network or [SSFN](https://perma.cc/PU5L-ALPM), is implemented as a SCION ISD, where a federation of three ISPs forms the ISD core.
Financial institutions are themselves SCION ASes and directly connect to one or more of the core ASes. Institutions deploy SCION–IP gateways (SIGs), transparently enabling their traditional IP-based applications to use the SCION network.
The concept of the SCION ISD also provides a mechanism to implement strict governance and access control (through the issuance of AS certificates).

Besides the SSFN, SCION connectivity has also been adopted by government entities for their international communications. In addition, Swiss higher education institutions are connected thanks to the [SCI-ED](http://scied.scion-architecture.net/) network.

In addition to productive deployments, SCION also comprises a global SCION research testbed called [SCIONLab](https://www.scionlab.org). It is composed of dozens of globally distributed infrastructure ASes, mostly run by academic institutions. The testbed is open to any user who can easily set up their own AS with the aid of a web-based UI, connect to the network, and run experiments. The setup has been the earliest global deployment of SCION and it has been supporting research and development of path-aware networking and SCION.

# IANA Considerations

Currently, this document has no request for action to IANA.
However, when full specification of SCION is available, requests for IANA actions are expected regarding the registration of optional packet header fields as well as the coordination of SCION ISD and AS number assignments.


# Security Considerations

SCION has been designed from the outset to offer security by default, and thus there are manifold security considerations. As a matter of fact, SCION's protocol design has been formally verified and the open source router implementation is undergoing formal verification (see also {{KLENZE2021}}). Describing all security considerations here, therefore, would go beyond the scope of this document. A separate document including all security implications and considerations will follow later.

--- back

# Acknowledgments
{:numbered="false"}

Many thanks go to Cyrill Krähenbühl, Juan A. Garcia-Pardo, and Kevin Meynell for reviewing this document. We are also indebted to Laurent Chuat, Markus Legner, David Basin, David Hausheer, Samuel Hitz, and Peter Müller, for writing the book "The Complete Guide to SCION" (see {{CHUAT22}}), which provides the background information needed to write this informational draft.

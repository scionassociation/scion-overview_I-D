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
  mail: panrg@irtf.org
  arch: https://datatracker.ietf.org/rg/panrg
  github: scionfoundation/scion-overview_I-D
  latest: https://example.com/LATEST

author:
 -   ins: C. de Kater
     name: Corine de Kater
     org: ETH Zuerich
     email: corine.dekatermuehlhaeuser@inf.ethz.ch

 -   ins: N. Rustignoli
     name: Nicola Rustignoli
     org: ETH Zuerich
     email: nicola.rustignoli@inf.ethz.ch

 -   ins: A. Perrig
     name: Adrian Perrig
     org: ETH Zuerich
     email: adrian.perrig@inf.ethz.ch

normative:


informative:
  RFC4264:
  RFC4033:
  RFC5218:
  RFC6480:
  RFC6830:
  RFC6996:
  RFC8205:
  RFC8446:
  RFC9049:
  RFC9217:
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
  KWON2021: DOI.10.1109/ICNP49622.2020.9259355
  ANDERSEN2001: DOI.10.1145/502034.502048
  KATZ2012: DOI.10.1145/2377677.2377756
  KUSHMAN2007: DOI.10.1145/1232919.1232927
  FISCHER2009: DOI.10.1145/1073814.1073868
  SHAIKH2001: DOI.10.1109/90.917073
  SCHERRER2020: DOI.10.1145/3453953.3453956


--- abstract

The Internet has been successful beyond even the most optimistic expectations and is intertwined with many aspects of our society. Unfortunately, the security of today’s Internet is far from commensurate with its importance as critical infrastructure. Additionally, the Internet has not primarily been built for high availability in the presence of adversaries, and recent proposals to improve Internet security and availability have been constrained by the setup of the current architecture.

The next-generation inter-network architecture SCION (Scalability, Control, and Isolation On Next-generation networks) aims to address the above-mentioned issues. SCION was explicitly designed from the outset to offer availability and security by default. The architecture provides route control, failure isolation, and explicit trust information for end-to-end communication. It also enables multi-path routing between hosts.

This document discusses the motivations behind the SCION architecture and gives a high-level overview of its fundamental components, including its authentication model and the setup of the control- and data plane. As SCION is already in production use today, the document concludes with an overview of SCION deployments.


--- middle

# Introduction

The Internet has been incredibly successful as it grew to a planet-scale network with billions of devices. But although this world-wide communication system guarantees global reachability, it falls short of providing other properties that are in demand today. These shortcomings of the current Internet are the reason for developing SCION: To make the Internet more secure, reliable, transparent, and scalable.

The Introduction section explores the motivation to develop SCION, followed by a short description of SCION's main elements. The sections after the Introduction provide deeper insight into SCION's key concepts and deployment scenarios. The document concludes with some concrete case studies where SCION has been successfully deployed in production.

## Why SCION - Motivation {#why}

Since its introduction back in the 1980s, the Internet has never stopped to expand. As a consequence, the global network continually needs to accommodate new uses. This has brought many issues to light, including a lack of transparency and control, poor scalability, occurrences of severe outages, weak fault isolation, and energy consumption. As the Internet has not been built with security in mind, the lack thereof is another problem. Because of this, the current Internet offers little protection against attacks such as spoofing, prefix- and DNS-hijacking, denial-of-service, and combinations of these. For more background information, see {{SCHUCHARD2011}}, {{LABOVITZ2000}}, {{GRIFFIN1999}}, {{SAHOO2009}}, and {{RFC4264}}.

Up until now, there have been numerous initiatives to address the above issues (e.g., {{RFC4033}}, {{RFC6480}}, {{RFC8205}}, and {{RFC8446}}). Although these initiatives have brought many improvements, concerns regarding security and scalability still remain (see, for example, {{LYCHEV2013}}, {{LI2014}}, {{COOPER2013}}, {{ROTHENBERGER2017}}, and {{MORILLO2021}}). Also other requirements that users have of today's Internet are not fulfilled yet (see, among others, [draft-king-irtf-challenges-in-routing](https://datatracker.ietf.org/doc/draft-king-irtf-challenges-in-routing/)). This especially pertains to the demands of enterprises globally exchanging sensitive information with an ecosystem, such as financial institutions, healthcare providers, universities, multinationals, governments, critical and transportation infrastructure operators.

These users require the Internet to be highly available at all times and constantly perform on a high level. They expect reliable operation of the global network also in case of failures, by the use of multi-path routing. They want to send their sensitive data packets over a secure and trustworthy networking infrastructure, and therefore prefer to select themselves the path their data will take. They also need availability guarantees across multiple routing domains, even in the presence of attacks. They further want to rely on an Internet that can be multilaterally governed and is free from global kill-switches. In short, today's users of the Internet seek performance, control, reliability, security, and trust.

SCION has been developed in order to meet the above-mentioned requirements. SCION aims to reach the following goals:

- Address the Internet's fundamental issues by offering
  - high availability also in the presence of adversaries,
  - fast failover in the case of faulty connections, and
  - prevention from hijacking, DoS, and other attacks.
- Make the Internet more transparent and efficient.
- Improve the Internet's scalability.
- Prepare the Internet for tomorrow's applications, such as virtual reality, Internet of Things (IoT), and Distributed Ledger Technology (DLT).

**Note**: A more detailed motivation for developing SCION will be described in a separate gap analysis internet draft.


### Avoiding Pitfalls

Of course SCION is not the first concept that addresses the Internet's networking issues. But unfortunately many other promising solutions for the Internet's problems have never managed to succeed, for reasons described in {{RFC9049}}. SCION, however, avoids the pitfalls mentioned in this document. For example, SCION does not have to be adopted by the entire Internet to be effective: The routing architecture provides benefits already to early adapters. Even if only a small part of the global network works with SCION, adapters will still take advantage of using the SCION routing technology. Moreover, not only users of SCION benefit from it, also ISPs and operators benefit from deploying SCION: early deployments showed that providers can charge the use of SCION as premium connectivity, with users who are willing to pay for it. Furthermore, SCION can be installed on top of and function alongside the existing routing infrastructure and protocols--there is no need for bigger changes in an operational network.

The above points facilitate the deployment of SCION and increase its acceptance. The several cases where SCION is already successfully implemented today illustrate this (see [Deployments](#deploy)).

### Why Now?

SCION can be considered a _path-aware internetworking_ architecture, as described in {{RFC9217}}. This RFC, which was published in March of this year (2022), poses (open) questions that must be answered in order to realize such a path-aware networking system. It was originally written to frame discussions in the Path Aware Networking Research Group (PANRG), and has been published to snapshot current thinking in this space.

SCION clearly provides answers to the questions raised in this RFC. This especially pertains to the second, third, seventh, and eighth question:

- How do endpoints and applications get access to accurate, useful, and trustworthy path properties?
- How can endpoints select paths to use for traffic in a way that can be trusted by the network, the endpoints, and the applications using them?
- How can a path-aware network in a path-aware internetwork be effectively operated, given control inputs from network administrators, application designers, and end users?
- How can the incentives of network operators and end users be aligned to realize the vision of path-aware networking, and how can the transition from current ("path-oblivious") to path-aware networking be managed?

The answers to these questions can be found in [Key Concepts](#key) and [Deployments](#deploy), respectively.

Another RFC that must be mentioned in the context of this draft is {{RFC5218}}, "What Makes for a Successful Protocol?". SCION fulfils most factors that contribute to the success of a protocol, as described in section 2.1 of the RFC. This includes such factors as offering a positive net value (i.e., the benefits of deploying SCION outweigh the costs), incremental deployability, and open source code availability. More importantly, SCION averts the failure criteria mentioned in section 1.4 of the RFC: SCION is already deployed and in use by many actors of the Swiss financial and academic ecosystems, and mainstream implementation of SCION is possible, too.

To conclude: The time is ripe to take SCION to the IETF, in order to contribute to the important discussion regarding path-aware networking, and to make a first step towards standardization.


## SCION Overview

SCION has been designed to address the fundamental issues of today's Internet depicted in [Why SCION - Motivation](#why). The following section gives a high-level overview of SCION's main elements, providing a basic understanding of this next-generation inter-network architecture.

### Network Architecture and Naming

SCION's main goal is to offer highly available and efficient inter-domain packet delivery—even in the presence of actively malicious entities. To achieve scalability and sovereignty, SCION organizes existing ASes into groups of independent routing planes, called **Isolation Domains (ISD)**. An AS can be a member of multiple ISDs. All ASes in an ISD agree on a set of trust roots, called the **Trust Root Configuration (TRC)**, ensuring that network traffic only flows on policy-compliant paths. The ISD is governed by a set of **core ASes**, which provide connectivity to other ISDs and manage the trust roots. Typically, the 3–10 largest ASes of an ISD form the ISD’s core.

Isolation domains serve the following purposes:

- They allow SCION to support trust heterogeneity, as each ISD can independently define its roots of trust;
- They provide transparency for trust relationships;
- They isolate the routing process within an ISD from external influences such as attacks and misconfigurations; and
- They improve the scalability of the routing protocol by separating it into a process within and one between ISDs.

ISDs provide natural isolation of routing failures and misconfigurations, give endpoints strong control over both inbound and outbound traffic, provide meaningful and enforceable trust, and enable scalable routing updates with high path-freshness.


#### Links

There are three types of links in SCION: core links, parent-child links, and peering links.

- A **core link** can only exist between two core ASes.
- A **parent-child link** requires that at least one of the two connected ASes is a non-core AS. ASes with a parent-child link usually belong to the same entity or have a provider-customer relationship.
- A **peering link** also includes at least one non-core AS. A peering link exists between ASes with a (standard or paid) relationship.

See {{architecture}} for a high-level overview of the SCION network structure.

~~~~
    ...............................
   :                               :
  :      [TCR]                      :
 :          (::::::::::::::)         :      ..........................
:        (::::: ISD core :::::)       :    :                          :
:    (:: +---+ ::::::::: +---+ ::)    :   :    [TCR]                   :
: (::::: |CAS|===+---+ : |CAS| :::::) :  :        (:: ISD core ::)      :
:    (:: +---+ : |CAS|===+---+====)===:==:=====(===+---+ ::: +---+ ::)  :
:       /(:::::: +---+ ::::::) \      :  :    (::: |CAS|=====|CAS| :::) :
:      /  (::::::: | :::::::)   \     :  :     (:: +---+ ::: +---+ ::)  :
:     /            |             o    :  :       /(::::::::::::::)\     :
:    o             |           +---+  :  :      /                  \    :
:  +---+           |          /|ASb|  :  :     /                    o   :
:  |ASa|           |         / +---+  :  :    o                   +---+ :
:  +---+           |        /    |    :  :  +---+                 |ASy| :
:    |             |       /     |    :  :  |ASx| --------------- +---+ :
:    |             |      /      o    :  :  +---+                       :
:    o             o     /     +---+  :  :    |                         :
:  +---+         +---+  /      |ASe|  :  :    o                         :
:  |ASc|---------|ASd| o       +---+ -:--:--+---+                       :
:  +---+         +---+                :  :  |ASz|           ISD 2       :
 :                                   :    : +---+                      :
  :            ISD 1                :      :                          :
   .................................        ..........................

    |
    |
    o  Parent AS - child AS    ----  Peering link    ===  Core link
~~~~
{: #architecture title="SCION network structure"}



### Routing

SCION operates on two routing levels: intra-ISD and inter-ISD. As a path-based architecture, SCION end hosts learn about available network path segments through **path-segment construction beacons (PCBs)**. A PCB is initiated by a core AS and then disseminated either within an ISD (to explore intra-ISD paths) or among core ASes (to explore core paths across different ISDs). The PCBs accumulate cryptographically protected path- and forwarding information on AS-level, and store this information in the form of **hop fields (HFs)**. End hosts use the information from these PCBs/hop fields to create end-to-end forwarding paths for data packets, who carry this information in their packet headers. This concept is called **packet-carried forwarding state (PCFS)**. The concept also supports multi-path communication among end hosts.

The process of creating an end-to-end forwarding path consists of the following steps:

1. First, an AS discovers paths to other ASes, during the *path exploration* (or beaconing) phase.
2. The AS then selects a few PCBs according to defined policies, transforms the selected PCBs into path segments, and registers these segments with a path infrastructure, thus making them available to other ASes. This happens during the *path registration* phase.
3. During the *path resolution* phase, the actual creation of an end-to-end forwarding path to the destination takes place. For this, an end host performs (a) a *path lookup* step, to obtain path segments, and (b) a *path combination* step, to combine the forwarding path from the segments.

{{beaconing}} below shows the SCION routing process in a nutshell.

~~~~
+------------------+             +------------------+
| Path Exploration |             |                  |
|   (Beaconing)    |------------>|Path Registration |
|                  |             |                  |
+------------------+             +--------+---------+
                                          |
                        +-----------------+
                        |
     +------------------v-----------------------+
     |            Path Resolution               |
     |+--------------+     +-------------------+|
     || Path Lookup  |---->| Path Combination  ||
     |+--------------+     +-------------------+|
     +------------------------------------------+
~~~~
{: #beaconing title="SCION routing in a nutshell"}


#### ISD and AS numbering

SCION decouples end-host addressing from inter-domain routing. Routing is based on the <ISD, AS> tuple, agnostic of end-host addressing. Existing AS numbers are inherited from the current Internet, but a 48-bit namespace allows for additional SCION AS numbers beyond the 32-bit space in use today. The end host local address is not used for inter-domain routing or forwarding, does not need to be globally unique, and can thus be an IPv4, IPv6, or MAC address, for example. A SCION address is therefore composed of the <ISD, AS, local address> 3-tuple.

For more details, see [IANA Considerations](#iana).

### Infrastructure Components {#infra-components}

The **beacon service**, the **path service**, and the **certificate service** are the main infrastructure components within a SCION AS. Each service can be deployed redundantly, depending on the AS's size and type. It is also possible to combine the services into one or more _control services_. _Internal routers_ forward packets inside the AS, while _border routers_ provide interconnectivity between ASes.

- The _beacon service_ discovers path information. It is responsible for generating, receiving, and propagating PCBs. Periodically, the beacon service generates a set of PCBs, which are forwarded to its child ASes or neighboring core ASes. The PCBs are flooded over policy-compliant paths to discover multiple paths between any pair of core ASes.
- The _path service_ stores mappings from AS identifiers to sets of announced path segments. The path service is organized as a hierarchical caching system similar to that of DNS. Through the beacon service, ASes select the set of path segments through which they want to be reached, and they register them to the path service in the ISD core.
- The _certificate service_ keeps cached copies of certificates and manages keys and certificates for securing inter-AS communication. The certificate service is queried by the beacon service when validating the authenticity of PCBs (i.e., when the beacon service lacks a certificate).

_Border routers_ are deployed at the edge of SCION ASes. The main task of border routers is to forward packets to a neighbor border router or to the destination host within the AS. While SCION takes care of inter-domain routing, it relies on existing routing protocols (e.g., IS-IS, OSPF, SDN) and communication fabric (e.g., IP, MPLS) for intra-domain forwarding. _Internal routers_, therefore, do not need to be changed to support SCION.

### Formal Verification

An additional feature of SCION is its formal verification. The SCION network system consists of a variety of components such as routers, servers, and edge devices. Such a complex system eludes the mental capacities of human beings for considering all possible states and interactions. That is why SCION includes a formal verification framework developed by the Department of Computer Science of the ETH Zurich {{KLENZE2021}}. This guarantees that packet forwarding and SCION's authentication mechanisms are correct and consistent.


## Conventions and Definitions

{::boilerplate bcp14-tagged}


# Key Concepts {#key}

This section explains the SCION key concepts, including authentication, control- and data plane.

## Authentication

SCION's control plane relies on a public-key infrastructure called the **control-plane PKI (CP-PKI)**, which is organized on ISD-level. Each ISD can independently build its own roots of trust, defined in a file called **trust root configuration (TRC)**.

**Note**: This section describes the SCION authentication concept on a very high level. A much more detailed description of SCION's authentication will follow in a separate internet draft.


### The Control-Plane PKI (CP-PKI)

Trust within each isolation domain is anchored in the trust root configuration (TRC) file. Each TRC contains a collection of signed root certificates, which are used to sign CA certificates, which are in turn used to sign AS certificates. The TRC also includes ISD-policies that specify, for example, the TRC's usage, validity, and future updates. TRCs are the main components of the CP-PKI.

The initial TRC in an ISD is called the **base TRC**. This base TRC constitutes the ISD's trust anchor. It is signed during a signing ceremony and then distributed throughout the ISD. All entities within the ISD obtain the initial TRC with an offline mechanism such as a USB flash drive provided by the ISP, or with an online mechanism that relies on a trust-on-first-use (TOFU) approach. However, all updates to the base TRCs are performed in a straightforward process that does not require any manual or out-of-band action (such as a software update), see [TRC Update and Verification](#update).

{{chain}} shows the TRC trust chain and associated certificates. TRC 1 is the base TRC, and TRC 2 and 3 constitute updates to this base TRC. TRC 2 must be verified using the voting certificates in TRC 1. Control-plane (CP) root certificates are used to verify other CP certificates (which are in turn used to verify path-segment construction beacons PCBs).

Each SCION AS must hold a private key (to sign PCBs) and a certificate attesting that it is the rightful owner of the corresponding public key. One of the main roles of the TRC is thus enabling the verification of **AS certificates** and PCBs.

~~~~
                +---------------------------------------------+
                |                    TRC 2                    |
                |+-------------------------------------------+|
                ||- Version   - Grace Period - No Trust Reset||
                ||- ID        - Core ASes    - Voting Quorum ||
+---------+     ||- Validity  - Description  - ...           ||    +---------+
|  TRC 1  |     |+-------------------------------------------+|    |  TRC 3  |
|  (Base  |---->|+--------------------+ +--------------------+|--->|         |
|  TRC)   |     ||   Regular Voting   | |  Sensitive Voting  ||    |         |
+---------+     ||    Certificate     | |    Certificate     ||    +---------+
                |+--------------------+ +--------------------+|
                |+--------------------+ +--------------------+|
                ||       Votes        | |     Signatures     ||
                |+--------------------+ +--------------------+|
                |+-------------------------------------------+|
                ||           CP Root Certificates            ||
                |+---------------+-------------+-------------+|
                |                |             |              |
                +----------------+-------------+--------------+
                                 |             |
                       +---------v-+         +-v---------+
                       |   CP CA   |         |   CP CA   |
                       |Certificate|         |Certificate|
                       +-+-------+-+         +-----+-----+
                         |       |                 |
                         |       |                 |
                +--------v--+ +--v--------+      +-v---------+
                |   CP AS   | |   CP AS   |      |   CP AS   |
                |Certificate| |Certificate|      |Certificate|
                +-----------+ +-----------+      +-----------+
~~~~
{: #chain title="TRC contents and trust chain"}


### TRC Update and Verification {#update}

With a base TRC as trust anchor, TRCs can be updated in a verifiable manner. There are two kinds of TRC updates: regular and sensitive updates. A _regular_ TRC update happens when the TRC's validity period expires. This period is defined by the _validity_ parameter in the TRC. The default is one year. A TRC update is _sensitive_ if and only if critical sections of the TRC are affected (for example, if the set of core ASes is modified). For both regular and sensitive TRC updates, a number of votes (in the form of signatures) must be cast to approve the update. This number of votes is dictated by the voting quorum and set in each TRC with the _voting quorum_ parameter.


### Dissemination of TRC Updates

Information about a TRC update is disseminated via the SCION’s beaconing process, through the path-segment constructions beacons. Each PCB contains the version number of the currently active TRC. If an AS receives a PCB with a TRC version number higher than the locally stored TRC, it requests the PCB-sending AS for the new TRC. The new TRC is verified on the basis of the current one, and is accepted if it contains at least the required quorum of correct signatures by trust roots defined in the current TRC.
This simple dissemination mechanism has two advantages: It is very efficient (as fresh PCBs rapidly reach all ASes), and it avoids circular dependencies with regard to the verification of PCBs and the beaconing process itself (as no server needs to be contacted over unknown paths in order to fetch the updated TRC).


### Grace Period

At most two TRCs per ISD can be active at the same time. The TRC parameter _grace period_ indicates for how long the currently active TRC can still be active after a new TRC is disseminated. This so-called **grace period** starts at the beginning of the validity period of the new TRC. An older TRC can only be active until either (1) the grace period has passed, or (2) yet a newer TRC is announced. AS certificates are validated by following the chain of trust up to an active TRC.


### Revocation and Recovery from a Catastrophic Event

The TRC dissemination mechanism also enables rapid revocation of trust roots. When a trust root is compromised, the other trust roots can remove it from the TRC and disseminate a new TRC alongside a PCB with a new version number.

In case of a catastrophic event—such as several private root keys being disclosed due to a critical vulnerability in a cryptographic library—SCION is equipped with a recovery procedure called **trust reset**. This procedure consists of creating a new TRC with fresh, trustworthy keys (and potentially new algorithms), and redistributing this TRC out-of-band. A trust reset effectively establishes a new base TRC for the ISD. It is possible for ISDs to disable trust resets by setting the _no trust reset_ Boolean parameter to "true" in their TRC, with the effect that the entire ISD would have to be abandoned in the event of such a catastrophic compromise (this abandonment would also have to be announced out-of-band).

The partition of the SCION network into ISDs guarantees that no single entity can take down the entire network. Even if several entities formed a coalition to carry out an attack, the effects of that attack would be limited to one or a few ISDs. Moreover, all actions are publicly visible, which deters misbehavior.

## SCION Control Plane

The SCION control plane is responsible for discovering path segments and making them available to end hosts. This process includes path exploration, registration, and lookup; it involves the path service, beacon service, and certificate service, both in core ASes and non-core ASes.

**Note**: This section describes the SCION control plane on a very high level. A much more detailed description of SCION's control plane will follow in a separate internet draft.

### Path Exploration

In SCION, the path segment construction process or routing is referred to as **beaconing**. Responsible for the beaconing process is the _beacon service_ of each AS, which generates, receives, and propagates the **path-segment construction beacons (PCBs)** on a regular bases, to iteratively construct path segments.

There are three types of path segments:

- A path segment from a non-core AS to a core AS is an _up-segment_.
- A path segment from a core AS to a non-core AS is a _down-segment_.
- A path segment between core ASes is a _core-segment_.

Up-segments and down-segments are invertible: An up-segment can be converted to a down-segment and vice versa, depending on the direction of the end-to-end path.

Path segment construction is conducted hierarchically on two levels:

- _Core beaconing_ is the process of constructing path segments between core ASes. During core beaconing, the beacon service of a core AS either initiates PCBs or propagates PCBs received from neighboring core ASes to all other neighboring core ASes. Core beaconing in SCION is similar to BGP’s route-advertising process, although in SCION the process is periodic and PCBs are flooded over policy-compliant paths to discover multiple paths between any pair of core ASes.
- _Intra-ISD beaconing_ creates path segments from core ASes to non-core ASes. For this, the beacon service of a core AS creates PCBs and sends them to the non-core child ASes (typically customer ASes). The beacon service of a non-core child AS receives these PCBs and forwards them to the AS's child ASes, and so on. This procedure continues until the PCB reaches an AS without any customer (leaf AS). As a result, all ASes receive path segments to reach the core ASes of their ISD.

On its way down, a PCB accumulates cryptographically protected path- and forwarding information on AS-level. At every AS, metadata as well as information about the AS's ingress and egress interfaces (i.e., link identifiers) is added to the PCB. The ingress and egress interface IDs identify connections to neighboring ASes. These IDs only need to be unique within each AS. Therefore, they can be chosen and encoded by each AS independently and without any need for coordination.

SCION also supports shortcuts and peering links. In a _shortcut_, a path only contains an up-path and a down-path segment, which can cross over at a non-core AS that is common to both paths. _Peering links_ can be added to up- or down-path segments, resulting in an operation similar to today’s Internet.

To reduce beaconing overhead and prevent possible forwarding loops, PCBs do not traverse peering links. Instead, peering links are announced along with a regular path in a PCB. If the path segments of both ASes at the end of a peering link contain this peering link, then it is possible to use the peering link to shortcut the end-to-end path (i.e., without going through the core). SCION also supports peering links that cross ISD boundaries, according to SCION’s path transparency property: A source knows the exact set of ASes and ISDs traversed during the delivery of a packet.

{{pcb}} shows how intra-ISD PCB propagation works, from the ISD core down to child ASes. For the sake of illustration, the interfaces of each AS are numbered with integer values. In practice, each AS can choose any encoding for its interfaces; in fact, only the AS itself needs to understand its encoding. Here, AS F receives two different PCBs via two different links from a core AS. Moreover, AS F uses two different links to send two different PCBs to AS G, each containing the respective egress interfaces. AS G extends the two PCBs and forwards both of them over a single link to a child AS.

~~~~
                                  .-----.
                                 ;  Core :
                        +-----+  :       ;
                        |PCB  |   \ 2 1 / +-----+
                        |Core |    `+-+'  |pcb  |
                        |Out:2|     | |   |core |
                        +--+--+   +-+ |   |out:1|
                           |      |   |   +--+--+
                           v      |   |      |
                                .-+---+.     v
                   .---.       /  2   3 \             .---.
                  (  J  )- - -; 1      4 :- - - - - -(  H  )
                   `---'      :   AS F   ;            `---'
                            +--\7       /
+----------+ +----------+ <-+     6  5
|PCB       | |pcb       |        `+--+'
|Core      | |core      |         |  |
|Out:2     | |out:1     |         |  |
|----------| |----------|         |  |
|AS F      | |as f      |         |  |
|In:2 Out:7| |in:3 out:7|         |  |
|Peer J:1  | |peer j:1  |         |  | +----------+ +----------+
|Peer H:4  | |peer h:4  |         |  | |PCB       | |pcb       |
|          | |          |         |  | |Core      | |core      |
+--+-------+ +--+-------+         |  | |Out:2     | |out:1     |
   |            |                 |  | |----------| |----------|
  <+           <+                 |  | |AS F      | |as f      |
                                  |  | |In:2 Out:5| |in:3 out:5|
         +----------+ +----------+|  | |Peer J:1  | |peer j:1  |
         |PCB       | |pcb       ||  | |Peer H:4  | |peer h:4  |
         |Core      | |core      ||  | |          | |          |
         |Out:2     | |out:1     ||  | +----+-----+ +----+-----+
         |----------| |----------||  |      |            |
         |AS F      | |as f      ||  |      v            v
         |In:2 Out:6| |in:3 out:6||  |
         |Peer J:1  | |peer j:1  ||  |
         |Peer H:4  | |peer h:4  ||  |
         |          | |          ||  |
         +----+-----+ +----+-----+|  |
              |            |     .+--+-.
              v            v   ,' 5  1  `.
                              ;           :
                              :   AS G    ;
                               \         /
                            +---` 4  3 ,'
                          <-+     `--+'
                                     |  +----------+ +----------+
                                     |  |PCB       | |pcb       |
                                     |  |Core      | |core      |
                                     |  |Out:2     | |out:1     |
           +----------+ +----------+ |  |----------| |----------|
           |PCB       | |pcb       | |  |AS F      | |as f      |
           |Core      | |core      | |  |In:2 Out:5| |in:3 out:5|
           |Out:2     | |out:1     | |  |Peer J:1  | |peer j:1  |
           |----------| |----------| |  |Peer H:4  | |peer h:4  |
           |AS F      | |as f      | |  |----------| |----------|
           |In:2 Out:6| |in:3 out:6| |  |AS G      | |as g      |
           |Peer J:1  | |peer j:1  | |  |In:1 Out:3| |in:1 out:3|
           |Peer H:4  | |peer h:4  | |  |          | |          |
           |----------| |----------| |  +----+-----+ +----+-----+
           |AS G      | |as g      | |       |            |
           |In:5 Out:3| |in:5 out:3| v       v            v
           |          | |          |
           +----+-----+ +----+-----+
                |            |
                v            v
~~~~
{: #pcb title="Intra-ISD PCB propagation from the ISD core down to child ASes"}

#### Security

Each PCB contains signatures of all on-path ASes. Every time a beacon service receives a PCB, it validates the PCB's authenticity. During this process, the beacon service can query the certificate service, for example, when the beacon service lacks a certificate.

#### Policies

Each AS can independently set policies dictating which PCBs are sent in which time intervals, and to which neighbors. In particular, PCBs do not need to be propagated immediately upon arrival. However, during bootstrapping and if the AS obtains a PCB containing a previously unknown path, the AS should forward the PCB immediately, such that other ASes learn about it quickly.


### Path Registration

Both the beacon service and the path service are involved in the path registration process. A non-core AS typically receives several PCBs representing several path segments to various core ASes. Out of these PCBs, the non-core AS must select those down-segments through which it wants to be reached. It is the task of the AS's beacon service to make this selection, according to the criteria described in [Path-Segment Selection](#selection). The beacon service then registers these path segments at the path service of the respective core AS. When links fail, segments expire, or better segments become available, the beacon service keeps updating the down-segments registered for its AS.

As a result, a core AS’s path service contains all the intra-ISD path segments registered by the leaf ASes of its ISD. In addition, a core AS path service also stores the preferred core-path segments to other core ASes.

Also each non-core AS includes a path service, as part of the AS's control service. A path service in a non-core AS contains up-segments to the core ASes of the ISD. The path services learn these up-segments by extracting them from the PCBs they obtain from their local beacon service. The global path infrastructure thus bears similarities to DNS, where information is fetched on-demand only.

#### Path-Segment Selection {#selection}

Among the received PCBs, the beacon service of an AS must choose (1) a set of PCBs to propagate further, and (2) a set of path segments to register. The selection of these PCBs and path segments is based on a path quality metric. This metric aims at identifying consistent, diverse, efficient, and policy-compliant paths:

- _Consistency_ implies that at least one property along the path is uniform, such as an AS capability (e.g., high bandwidth).
- _Diversity_ means that the set of paths announced over time are as path-disjoint as possible, in order to provide high-quality multipath options.
- _Efficiency_ refers to the length, bandwidth, latency, utilization, and availability of a path, where more efficient paths are naturally preferred.
- _Policy compliance_ implies that the path adheres to the AS’s routing policy.

Based on past PCBs, the AS beacon service assigns scores to the current set of candidate path segments, and sends the best segments in the next beaconing interval.

Core beaconing operates similarly to intra-ISD beaconing, except that core PCBs only traverse core ASes. The same path selection metrics apply, where a core AS attempts to forward the set of most desirable paths to its neighbors.

### Path Lookup

An end host (source) who wants to start communication with another host (destination), requires up to three path segments: An up-segment to reach the ISD core, a core-segment to reach the destination ISD, and a down-segment to reach the destination AS. The source host queries the path service in its AS for such segments. The path service has up-segments stored in its database and furthermore checks if it has appropriate core- and down-segments in its cache; in this case it returns them immediately.

If not, the path service in the source AS queries core path services (using locally stored up-segments) in the source ISD for core-segments to the destination ISD. Then, it combines up-segments with the newly retrieved core-segments, and queries core path services in the remote ISD to fetch remote down-segments. To improve overall efficiency, the local path service caches the returned path segments and uses parallelism when requesting path segments from core path services. Finally, the local path service returns all path segments to the source host.

This recursive lookup strongly simplifies the process for end hosts (which only have to send a single query, similar to stub DNS resolvers). The caching strategy ensures that path lookups are fast for frequently used destinations (similar to caching in recursive DNS resolvers).

### Link Failures

Unlike in the current Internet, link failures are not automatically resolved by the network, but require active handling by end hosts. Since SCION forwarding paths are static, they break when one of the links fails. Link failures are handled by a two-pronged approach that typically masks link failures without any outage to the application and rapidly re-establishes fresh working paths:

- The SCION Control Message Protocol (SCMP) (the SCION equivalent of ICMP) is used for signaling connectivity problems. Instead of relying on application- or transport-layer timeouts, end hosts get immediate feedback from the network if a path stops working, and can quickly switch to an alternative path.
- SCION end hosts are encouraged to use multipath communication by default, thus masking a link failure with another working path. As multipath communication can increase availability (even in environments with very limited path choices), SCION beacon services attempt to create disjoint paths, SCION path services attempt to select and announce disjoint paths, and end hosts compose path segments to achieve maximum resilience to path failure. Consequently, most link failures in SCION remain unnoticed by the application, unlike the frequent (albeit mostly brief) outages in the current Internet. See also {{ANDERSEN2001}}, {{KATZ2012}}, and {{KUSHMAN2007}}, as well as [Demonstrating the reliability and resilience of Secure Swiss Finance Network](https://perma.cc/4H3Q-WZNG).


## SCION Data Plane

While the control plane is responsible for providing end-to-end paths, the data plane ensures that packets are forwarded on the selected path. SCION border routers forward packets to the next AS based on the AS-level path in the packet header (which is extended with ingress and egress interface identifiers for each AS), without inspecting the destination address and also without consulting an inter-domain forwarding table. Only the border router at the destination AS needs to inspect the destination address to forward it to the appropriate local end host.

Because SCION splits the information about the locator (the path towards the destination AS) and the identifier (the destination address), the identifier can have any format that the destination AS can interpret--only the destination needs to consider that local identifier (see also {{RFC6830}}). In other words, an AS can select an arbitrary addressing format for its hosts, e.g., a 4-byte IPv4, 6-byte media access control (MAC) address, 16-byte IPv6, or any other up to 16-byte addressing scheme. A valuable consequence is that hosts with different address types can directly communicate, e.g., an IPv4 host can communicate with an IPv6 host over SCION.

The next two sections describe how an end host combines path segments into an end-to-end forwarding path, and how border routers forward packets efficiently.

**Note**: This section describes the SCION data plane on a very high level. A much more detailed description of SCION's data plane will follow in a separate internet draft.

### Path Construction via Segment Combination

Through the path lookup, the end host obtains path segments that must be combined into an end-to-end path. A valid SCION **forwarding path** can be created by combining up to three path segments, in the following ways:

- **Immediate combination of path segments**: The last AS on the up-segment is also the first AS on the down-segment. In this case, the simple combination of an up-segment and a down-segment creates a valid forwarding path.
- **AS shortcut**: The up-segment and down-segment intersect at a non-core AS. In this case, a shorter forwarding path can be created by removing the extraneous part of the path.
- **Peering shortcut**: A peering link exists between the two segments, so a shortcut via the peering link is possible. As in the AS shortcut case, the extraneous path segment is cut off. The peering link could be traversing to a different ISD.
- **Combination with a core-segment**: The last AS on the up-segment is different from the first AS on the down-segment. This case requires an additional core-segment to connect the up- and down-segment. If the communication remains within the same ISD, a local ISD core-segment is needed; otherwise, an inter-ISD core-segment is required.
- **On-path**: The destination AS is part of the up-segment or the source AS is part of the down-segment; in this case, a single up- or down-segment, respectively, is sufficient to create a forwarding path.

Once a forwarding path is chosen, it is encoded in the SCION packet header. This makes inter-domain routing tables unnecessary for border routers: Both the ingress and the egress interface of each AS on the path are encoded as **packet-carried forwarding state (PCFS)** in the packet header. The destination can respond to the source by reversing the end-to-end path from the packet header, or it can perform its own path lookup and combination.

The SCION packet header consists of a sequence of **hop fields (HFs)**, one HF for each AS that is traversed on the end-to-end path. Each hop field contains the encoded numbers of the ingress and egress links, and thus defines which interfaces may be used to enter and leave an AS. In addition to the hop fields, each path segment contains an **info field (INF)** with basic information about the segment. A host can create an end-to-end forwarding path by extracting info fields and hop fields from path segments, as depicted in {{HFs}}. The additional meta header (META) contains pointers to the currently active INF and HF.

~~~~
up-segment             core-segment             down-segment

+-------+              +-------+                +-------+
|+-----+|              |+-----+|                |+-----+|
|+ INF ||----------+   |+ INF ||---+            |+ INF ||-+
|+-----+|          |   |+-----+|   |            |+-----+| |
|+-----+|          |   |+-----+|   |            |+-----+| |
|| hf  ||--------+ |   || hf  ||---+--+         || hf  ||-+--+
|+-----+|        | |   |+-----+|   |  |         |+-----+| |  |
|+-----+|        | |   |+-----+|   |  |         |+-----+| |  |
|| hf  ||-----+  | |   || hf  ||---+--+--+      || hf  ||-+--+--+
|+-----+|     |  | |   |+-----+|   |  |  |      |+-----+| |  |  |
|+-----+|     |  | |   +-------+   |  |  |      +-------+ |  |  |
|| hf  ||--+  |  | |               |  |  |                |  |  |
|+-----+|  |  |  | |   +--------+  |  |  |                |  |  |
+-------+  |  |  | |   |++-----+|  |  |  |                |  |  |
           |  |  | |   |++ Meta||  |  |  |                |  |  |
           |  |  | |   |++-----+|  |  |  |                |  |  |
           |  |  | |   |+-----+ |  |  |  |                |  |  |
           |  |  | +-->|+ INF | |  |  |  |                |  |  |
           |  |  |     |+-----+ |  |  |  |                |  |  |
           |  |  |     |+-----+ |  |  |  |                |  |  |
           |  |  |     |+ INF | |<-+  |  |                |  |  |
           |  |  |     |+-----+ |     |  |                |  |  |
           |  |  |     |+-----+ |     |  |                |  |  |
           |  |  |     |+ INF | |<----+--+----------------+  |  |
           |  |  |     |+-----+ |     |  |                   |  |
           |  |  |     |+-----+ |     |  |                   |  |
           |  |  +---->|| hf  | |     |  |                   |  |
           |  |        |+-----+ |     |  |                   |  |
           |  |        |+-----+ |     |  |                   |  |
           |  +------->|| hf  | |     |  |                   |  |
           |           |+-----+ |     |  |                   |  |
           |           |+-----+ |     |  |                   |  |
           +---------->|| hf  | |     |  |                   |  |
                       |+-----+ |     |  |                   |  |
                       |+-----+ |     |  |                   |  |
                       || hf  | |<----+  |                   |  |
                       |+-----+ |        |                   |  |
                       |+-----+ |        |                   |  |
                       || hf  | |<-------+                   |  |
                       |+-----+ |                            |  |
                       |+-----+ |                            |  |
                       || hf  | |<---------------------------+  |
                       |+-----+ |                               |
                       |+-----+ |                               |
                       || hf  | |<------------------------------+
                       |+-----+ |
                       +--------+
                     forwarding path
~~~~
{: #HFs title="Combining three path segments into a forwarding path"}


### Path Authorization

It is crucial for the data plane that end hosts only use paths constructed and authorized by ASes in the control plane. In particular, end hosts should not be able to craft HFs themselves, modify HFs in authorized path segments, or combine HFs of different path segments (path splicing). This property is called **path authorization** (see {{KLENZE2021}} and [EPIC: Every packet is checked in the data plane of a path-aware Internet](https://netsec.ethz.ch/publications/papers/Legner_Usenix2020_EPIC)).

SCION achieves path authorization by creating message-authentication codes (MACs) during the beaconing process. Each AS calculates these MACs using a local secret key (that is only shared between SCION infrastructure elements within the AS) and chains them to the previous HFs. The MACs are then included in the forwarding path as part of the respective HFs.

### Forwarding

Routers can efficiently forward packets in the SCION architecture. In particular, the absence of inter-domain routing tables and of complex longest-IP-prefix matching performed by current routers enables the construction of more efficient routers.

During packet forwarding, a SCION border router at the ingress point of the AS verifies that:

- the packet entered through the correct ingress interface corresponding to the information in the HF,
- the HF is still valid, and
- the MAC in the HF is correct.

If the packet has not yet reached the destination AS, the egress interface number in the HF of the non-destination AS refers to the egress SCION border router of this AS. In this case, the packet can be sent from the ingress SCION border router to the egress SCION border router via native intra-domain forwarding (e.g., IP or MPLS). In case the packet has arrived at the destination AS, the destination AS's border router inspects the destination address and sends the packet to the corresponding host.

### Intra-AS Communication

Communication within an AS is handled by existing intra-domain communication technologies and protocols such as IP with Software-Defined Networking (SDN), or Multiprotocol Label Switching (MPLS).



# Deployment
Deploying a next-generation architecture is a challenging task, as it needs to be integrated with and operate alongside existing infrastructure. In the following, we discuss practical deployment approaches, supporting both native SCION hosts and IP hosts.

## Autonomous System Deployment
A SCION AS needs to deploy the SCION [infrastructure components](#infra-components) and border routers. Practice shows that all of them can be deployed on standard x86 commercial off-the-shelf servers, supporting up to 100 Gbps links. With a P4 implementation hardware it is possible to forward SCION traffic even at terabit speeds {{DERUITER2021}}.
Within an AS, SCION is deployed as an IP overlay on top of the existing network. This way SCION allows, by design, to reuse the existing intra-domain network and equipment (i.e., IP, MPLS, ...). Customer-side SCION border routers directly connect to the provider-side border routers using last-mile connections. The SCION design assumes that AS’s internal entities are considered to be trustworthy, therefore the IP overlay or the first-hop routing does not compromise or degrade any security properties SCION delivers.
When it comes to inter-domain communication, an overlay deployment on top of today’s Internet is not desirable, as SCION would inherit issues from  its weak underlay. Thus, intra-AS SCION links are usually deployed in parallel to existing links, in order to preserve its security properties. That is, two SCION border routers are directly connected via a layer-2 cross-connection at a common point-of-presence, achieving connectivity with high reliability, availability, and performance.

TODO: sentences mentioning throughput seem a bit out of the blue here..  Also, maybe a figure showing customer/provider deployment might not be a bad idea?

## Internet Exchange Points
Internet Exchange Points (IXP) play an important role for SCION as they do in today’s Internet.  SCION can be deployed at existing IXPs following a "big switch" model, where the IXP provides a large L2 switch between multiple SCION ASes. SCION has been deployed following this model at the Swiss Internet Exchange (SwissIX),  currently interconnecting major SCION Swiss ISPs and enterprises through bi-lateral peering over a dedicated SCION port.

Additionally, thanks to its path-awareness, SCION offers the option of an enhanced deployment model. The internal topology of an IXP to be exposed within the SCION control plane. This enables IXP customers to use SCION’s multi-path and fast failover capabilities to leverage the IXP’s internal links (including backup links) and to select paths depending on the application’s needs.  IXPs have therefore an incentive to expose their rich internal connectivity as the benefits from SCION’s multi-path capabilities would increase their value for customers and provide them with a competitive advantage.

## End Hosts and Incremental Deployability
End-users can leverage SCION in two different ways: using SCION-aware applications on a [SCION native end host](#native-endhost), or using  transparent [IP-to-SCION conversion](#sig). The benefit of using SCION natively is that the full range of advantages becomes available to applications, at the cost of installing the SCION endpoint stack and making the application SCION-aware. In the short term, the second approach is preferred.

### Native End Hosts {#native-endhost}
A SCION native end-host's stack consists of a dispatcher, which handles all incoming and outgoing SCION packets, and of a SCION daemon, which handles control-plane messages. The latter  fetches paths to remote ASes and provides an API for applications and libraries to interact with the SCION control plane (i.e., for path lookup, SCION extensions). The current SCION implementation uses an UDP/IP underlay to communicate between end-hosts and SCION routers. This allows reuse of existing intra-domain networking infrastructure. SCION end-hosts can optionally use automated bootstrapping mechanisms to retrieve configuration from the network and establish SCION connectivity. This way clients require no pre-existing network-specific configurations.

### SCION to IP Gateway (SIG) {#sig}
A SCION-IP-Gateway (SIG) encapsulates regular IP packets into SCION packets with a corresponding SIG at the destination that performs the decapsulation.
A SIG can be deployed close to the end-user (i.e., at branches of an enterprise, on a CPE), or it can be deployed within an ISP's network. In the latter case, the SIG is called carrier-grade SIG, as it serves multiple customers within the AS where it is deployed. This approach has the advantage that it does not require any changes at the customer's premises.
In order to allow incremental deployability and to ease transition from legacy IP-based Internet to SCION, SIGs can be augmented with  mechanisms allowing them to coordinate and automatically exchange IP prefix information. A more detailed description of the SIG and its coordination mechanisms is to be presented in dedicated documents.



## Deployment experiences {#deploy}

SCION has been deployed in production by multiple entities, growing its acceptance among industry. While early deployments started on academic and research networks, SCION has expanded to serve the financial industry, government, and healthcare.

In 2017, SCION was evaluated for production use by a central bank, with the goal of modernising the network interconnecting banks and their branches in order to improve network flexibility and cut cost. Existing lines were provisioned via dedicated layer-2 circuit switching or layer-3 MPLS–is, providing availability and confidentiality. SCION approximates leased-line properties, offering geofencing, path transparency, high reliability thanks to fast failover, and flexibility, as it enables connectivity to any other entities connected to the SCION Internet. TODO: add link to press release: https://perma.cc/PU5L-ALPM

Positive experiences with early deployments led the Swiss financial industry to adopt its SCION connectivity to support system-critical applications, like the national real-time gross settlement (RTGS) system, connecting all country's banks to exchange real-time payment information.  The network, called Secure Swiss Finance Network (SSFN), is implemented as a SCION ISD, where the core is formed by a federation of three network service providers (core ASes) deploying SCION routers at the borders of their network.  Members of the SSFN—i.e., financial institutions, are directly connected to one or more of these core ASes. They are themselves SCION ASes that additionally deploy SCION–IP gateways (SIGs). These SIGs provide the entry points for members to use the SSFN as a communication platform—they transparently enable traditional IP-based communication to use a SCION network.

SCION connectivity has also been adopted by government entities for their international communications. In addition, Swiss higher education institutions are connected thanks to SCI-ED.

TODO: Link/reference SSFN, SCI-ED


Besides productive deployments, SCION also comprises a global SCION research testbed called {{KWON2021}}. Its is composed of a set of dozens of globally distributed infrastructure ASes, mostly run by academic institutions. The testbed is open to any user, who can easily set up their own AS with the aid of a web-based UI, connect to the network and run experiments. The setup has been the earliest global deployment of SCION, and it has been supporting research and development of path-aware networking and SCION.

# IANA Considerations {#iana}

Within the SCION ecosystem, each ISD-AS is identified with a 64-bit number; the most significant 16 bits identify the ISD (represented in decimal), the least significant 48 bits identify the AS in a format similar to that of IPv6 addresses, and a hyphen is used to separate the two—e.g., 4-ff00:1:f. In the remainder of this
section, we elaborate on the latter (i.e., the concrete numbering).

## ISD Numbers
ISDs are represented with decimal numbers, ranging from 0 to 65535. Table 2.1 shows the current allocation of ISD numbers. The ISD number 0 is reserved to mean “any ISD” and used notably during path lookup.

| ISD Number                       | Description                                      |
| -------------------------------- | ------------------------------------------------ |
| 0                                | Wildcard ISD (stands for “any ISD”) |
| 1–15                             | Reserved for documentation and sample code |
| 16–63                            | Private use (can be used for testing, analogously to {{RFC6996}} |
| 64–4094                          | Public ISDs, should be assigned in ascending order, without gaps and without vanity numbers |
| 4095–65535                       | Reserved |
{: #numbers title="Allocation and description of ISD number ranges"}

## AS Numbers

The SCION numbering scheme uses a superset of the existing BGP AS numbering scheme (see also [Autonomous system numbers](https://perma.cc/TEG2-8D3Z)). The default format for AS numbers is similar to IPv6. It uses a 16-bit colon separated lower-case hexadecimal encoding with leading zeros omitted. However, the double colon (::) zero-compression feature of IPv6 is not supported. As for ISD numbers, 0 represents the wildcard AS and stands for “any AS”, which may be used during path lookup.

The range from 1 to 232 - 1 is dedicated to BGP AS numbers. If a BGP AS supports SCION, it has the same AS number for both BGP and SCION. To facilitate the comparison with BGP AS numbers, any number in the BGP AS range is represented as a decimal. While it is legal to write a BGP AS number using the SCION syntax, programs should use the decimal representation for display. For example, if a program receives 0:1:f, it should display it as 65551.

Currently, the 2:0:0/16 range is allocated to public SCION-only ASes (i.e., ASes that are not existing BGP ASes). AS numbers in that range should be assigned in ascending order, without gaps and without vanity numbers.

## Assignment of ISD and AS Numbers

Ideally, each AS number should be globally unique (partly to facilitate the comparison and transition from BGP), but the actual requirement is only that each AS number be unique within an ISD. Since an AS can be part of several ISDs, picking a globally unique AS number also facilitates joining new ISDs.

In principle, ISD numbers can be self-assigned: A number that is not yet used by any other ISD is picked by the constituents of the new ISD before the first TRC is signed and distributed, then other ISDs are free to accept or reject the new TRC. Preferably, however, an organization such as ICANN or a regional Internet registry (e.g., RIPE NCC) will take on the responsibility of assigning ISD and AS numbers.

# Security Considerations

SCION seeks to achieve greater transparency and control for the forwarding paths of network packets, and the trust roots used for authentication. When the network offers path transparency, end hosts can predict (and verify) the forwarding path taken by packets.

Taking transparency of network paths as a first property, SCION aims to additionally achieve path control, a stronger property that (1) enables ASes to control the incoming path segments through which they are reachable and (2) allows senders to then create and select end-to-end paths. This seemingly benign requirement has several repercussions—beneficial but also fragile if implemented incorrectly. This section lists the fragile aspects that need to be handled with care.

- **Respecting the forwarding policies of ISPs**: If senders have complete path control, they may violate ISPs’ forwarding policies. It must therefore be ensured that ISPs offer a set of policy-compliant paths which senders can choose from.
- **Preventing malicious path creation**: A malicious sender could exploit path control for attacks, for example by forming malicious forwarding paths such as loops that consume increased network resources.
- **Network stability**: Past research has shown that uncoordinated path selection by end hosts can lead to persistent oscillations, i.e., an alternating grow-and-shrink pattern of traffic volumes on links (see {{FISCHER2009}}, {{SHAIKH2001}}). This is often raised as a key concern and represents one of the biggest obstacles to deployment of path-aware networks ({{RFC9049}}). It is thus imperative that a future Internet architecture take this into account and develop mechanisms preventing these instabilities ({{SCHERRER2020}}).

--- back

# Acknowledgments
{:numbered="false"}

Many thanks go to Cyrill Krähenbühl for his review of this document. We are also indebted to Laurent Chuat, Markus Legner, David Basin, David Hausheer, Samuel Hitz, Peter Müller, and Adrian Perrig, for writing the book "The Complete Guide to SCION", which provides all the background information needed to write this informational draft.

# Media Over QUIC Transport for DVB Services Using MPEG-2 Transport Stream Packaging

**A Technical Whitepaper on Deploying MOQ+M2TS Across DVB Satellite and Terrestrial Networks**

---

## Abstract

This whitepaper describes an architectural framework for carrying DVB services
over Media Over QUIC Transport (MOQT) using MPEG-2 Transport Stream and M2TS
source packets, as defined by the MSFTS packaging extension to the MOQT
Streaming Format (MSF). It covers the protocol stack integration with
DVB-S2/S2X, DVB-T2, and hybrid broadcast-broadband infrastructures; the role
of MSFTS catalog fields in describing DVB service tracks; and three deployment
scenarios spanning broadcast contribution, multicast distribution, and unicast
streaming. The paper analyses how MOQ+M2TS complements existing DVB-DASH and
DVB-NIP deployments, serves as a migration bridge for existing M2TS workflows,
and presents a path toward MOQ as a first-class DVB IP transport layer. No
implementation or vendor specifics are included.

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Background](#2-background)
   - 2.1 [MPEG-2 Transport Stream and M2TS](#21-mpeg-2-transport-stream-and-m2ts)
   - 2.2 [DVB-DASH](#22-dvb-dash)
   - 2.3 [DVB Native IP Broadcasting](#23-dvb-native-ip-broadcasting)
   - 2.4 [Media Over QUIC Transport](#24-media-over-quic-transport)
   - 2.5 [MOQT Streaming Format and MSFTS](#25-moqt-streaming-format-and-msfts)
3. [Protocol Stack](#3-protocol-stack)
4. [MSFTS Catalog Integration for DVB Services](#4-msfts-catalog-integration-for-dvb-services)
   - 4.1 [Single-Program Satellite Feed](#41-single-program-satellite-feed)
   - 4.2 [Multi-Program Terrestrial Mux](#42-multi-program-terrestrial-mux)
   - 4.3 [ABR Alternate Renditions](#43-abr-alternate-renditions)
   - 4.4 [SCTE-35 and Splice Signaling](#44-scte-35-and-splice-signaling)
5. [DVB Deployment Scenarios](#5-dvb-deployment-scenarios)
   - 5.1 [Satellite Contribution and Distribution (DVB-S2/S2X)](#51-satellite-contribution-and-distribution-dvb-s2s2x)
   - 5.2 [Terrestrial Multicast Distribution (DVB-T2)](#52-terrestrial-multicast-distribution-dvb-t2)
   - 5.3 [Hybrid Broadcast-Broadband (DVB-NIP + QUIC Unicast)](#53-hybrid-broadcast-broadband-dvb-nip--quic-unicast)
6. [Relationship to Existing DVB Standards](#6-relationship-to-existing-dvb-standards)
   - 6.1 [Complement](#61-complement)
   - 6.2 [Bridge](#62-bridge)
   - 6.3 [Replacement Path](#63-replacement-path)
7. [Standardization Path](#7-standardization-path)
   - 7.1 [IETF MOQ Working Group](#71-ietf-moq-working-group)
   - 7.2 [DVB](#72-dvb)
8. [Conclusion](#8-conclusion)
9. [References](#9-references)

---

## 1. Introduction

DVB has standardized IP-based service delivery through two complementary
specifications: DVB-DASH (ETSI EN 303 285), which defines a profile of MPEG DASH
for adaptive bitrate streaming of DVB services over IP networks using the ISO Base
Media File Format (ISO BMFF); and DVB Native IP Broadcasting (DVB-NIP, ETSI EN 303
560), which specifies end-to-end native IP broadcast over DVB satellite and
terrestrial bearers using Generic Stream Encapsulation (GSE) and multicast adaptive
bitrate delivery (DVB-MABR). Both specifications assume HTTP and TCP at the
application transport layer.

As live contribution and distribution latency requirements tighten — particularly
for sports, news, and event broadcasting — the characteristics of TCP become
operationally significant. TCP's reliable, ordered byte-stream delivery model
introduces head-of-line blocking: a single lost segment stalls delivery of all
subsequent data until retransmission completes, regardless of whether later data
could be rendered independently. HTTP request-response semantics compound this by
coupling the receiver's consumption rate to the server's delivery cadence, adding
latency at every transaction boundary.

QUIC (RFC 9000) addresses these constraints at the transport layer. QUIC provides
multiplexed streams over a single connection with independent loss recovery per
stream, connection migration, and significantly reduced handshake latency compared
to TLS over TCP. WebTransport extends QUIC's capabilities to browser endpoints.
Media Over QUIC Transport (MOQT, draft-ietf-moq-transport) builds on QUIC to
define an object-oriented publish-subscribe delivery model for media: publishers
produce named objects organized into tracks and groups; subscribers receive objects
with configurable reliability and priority; relays cache and forward objects using
only MOQT metadata, without parsing media payloads.

MPEG-2 Transport Stream (M2TS) is the media container format at the heart of
existing DVB contribution and distribution workflows. Encoders, muxers, playout
systems, conditional access headends, and terrestrial transmitters all operate on
M2TS. Any IP transport technology that requires re-packaging M2TS into a different
container — as DVB-DASH does with ISO BMFF — imposes an encoding boundary that
adds latency, complexity, and cost. The MSFTS extension to the MOQT Streaming
Format (draft-gregoire-moq-msfts) defines a packaging mode that carries M2TS
source packets directly as MOQT objects, without re-wrapping or re-encoding.

This paper describes the architectural framework for deploying MOQ+M2TS across
DVB satellite (DVB-S2/S2X) and terrestrial (DVB-T2) networks, including hybrid
broadcast-broadband topologies. It is addressed to two audiences: DVB member
organizations evaluating MOQ+M2TS as a candidate transport for future DVB
profiles, and IETF MOQ Working Group participants who need concrete DVB deployment
scenarios to understand the applicability of MSFTS. The paper is self-contained:
it provides sufficient background on MOQT, MSF, MSFTS, and DVB standards for
readers unfamiliar with any of them. No implementation or vendor specifics are
included.

## 2. Background

### 2.1 MPEG-2 Transport Stream and M2TS

<!-- TODO: Task 3 -->

### 2.2 DVB-DASH

<!-- TODO: Task 3 -->

### 2.3 DVB Native IP Broadcasting

<!-- TODO: Task 3 -->

### 2.4 Media Over QUIC Transport

<!-- TODO: Task 3 -->

### 2.5 MOQT Streaming Format and MSFTS

<!-- TODO: Task 3 -->

## 3. Protocol Stack

<!-- TODO: Task 4 -->

## 4. MSFTS Catalog Integration for DVB Services

### 4.1 Single-Program Satellite Feed

<!-- TODO: Task 5 -->

### 4.2 Multi-Program Terrestrial Mux

<!-- TODO: Task 5 -->

### 4.3 ABR Alternate Renditions

<!-- TODO: Task 5 -->

### 4.4 SCTE-35 and Splice Signaling

<!-- TODO: Task 5 -->

## 5. DVB Deployment Scenarios

### 5.1 Satellite Contribution and Distribution (DVB-S2/S2X)

<!-- TODO: Task 6 -->

### 5.2 Terrestrial Multicast Distribution (DVB-T2)

<!-- TODO: Task 6 -->

### 5.3 Hybrid Broadcast-Broadband (DVB-NIP + QUIC Unicast)

<!-- TODO: Task 6 -->

## 6. Relationship to Existing DVB Standards

### 6.1 Complement

<!-- TODO: Task 7 -->

### 6.2 Bridge

<!-- TODO: Task 7 -->

### 6.3 Replacement Path

<!-- TODO: Task 7 -->

## 7. Standardization Path

### 7.1 IETF MOQ Working Group

<!-- TODO: Task 8 -->

### 7.2 DVB

<!-- TODO: Task 8 -->

## 8. Conclusion

<!-- TODO: Task 9 -->

## 9. References

<!-- TODO: Task 10 -->

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

MPEG-2 Transport Stream (ISO/IEC 13818-1) is a packetized multiplex format
designed for reliable transmission of audio, video, and data over error-prone
channels. The fundamental unit is the TS packet: a fixed-length 188-octet
structure consisting of a 4-octet header followed by 184 octets of payload. The
header includes a sync byte (0x47), a 13-bit Packet Identifier (PID) identifying
the elementary stream or table carried in the packet, and control fields including
a 4-bit continuity counter for loss detection.

M2TS source packets extend the TS packet with a 4-octet source-packet timestamp
prefix, yielding a 192-octet structure. The timestamp records the arrival or
emission time of the TS packet and is used for System Time Clock (STC) recovery
at receiving equipment.

Program structure is described by Program Specific Information (PSI) tables
carried in-band. The Program Association Table (PAT, PID 0x0000) lists all
programs in the multiplex with pointers to their Program Map Tables (PMT). Each
PMT identifies the elementary streams (video, audio, subtitles, data) belonging
to its program and the PID carrying the Program Clock Reference (PCR) for timing
recovery. PTS (Presentation Timestamp) and DTS (Decode Timestamp) values embedded
in Packetized Elementary Stream (PES) headers synchronize audio and video
presentation. A transport stream whose PAT lists exactly one program is a
single-program transport stream (SPTS); one listing two or more programs is a
multi-program transport stream (MPTS).

SCTE-35 splice signaling is carried as splice_info_section() messages on a
designated PID registered in the PMT, enabling downstream systems to detect
program boundaries for dynamic ad insertion or content switching.

### 2.2 DVB-DASH

DVB-DASH (ETSI EN 303 285) defines a profile of MPEG Dynamic Adaptive Streaming
over HTTP (MPEG DASH, ISO/IEC 23009-1) for delivery of DVB television services
over IP networks. Media is packaged in ISO Base Media File Format (ISO BMFF)
fragmented MP4 containers and delivered via HTTP. Clients request segments at
bitrates matching their available bandwidth, enabling adaptive quality selection.

The DVB-DASH codec toolkit includes AVC (H.264), HEVC (H.265), and VVC (H.266)
for video; HE-AAC and AC-4 for audio. DVB-DASH supports HDTV, UHDTV, High
Dynamic Range (HDR), and High Frame Rate (HFR) content. Service discovery —
mapping service identifiers to DASH manifest URLs — is handled by DVB-I (ETSI TS
103 770). DVB provides a conformance validator and HDR test content for
interoperability testing.

### 2.3 DVB Native IP Broadcasting

DVB Native IP Broadcasting (DVB-NIP, ETSI EN 303 560) specifies an end-to-end
native IP broadcast system for DVB satellite (DVB-S2, DVB-S2X) and terrestrial
(DVB-T2) bearers. IP packets are encapsulated using Generic Stream Encapsulation
(GSE) with robust header compression and logical link control, enabling efficient
one-to-many IP delivery over broadcast physical layers.

DVB-NIP uses DVB Multicast ABR (DVB-MABR, ETSI TS 103 769) for adaptive bitrate
delivery over the broadcast path. DVB-MABR delivers DASH segments via multicast,
allowing receivers to adapt quality without unicast round-trips. DVB-NIP
integrates with DVB-I for service discovery and DVB-DASH for media streaming,
forming a layered stack from physical bearer to application. Hybrid
broadcast-broadband architectures combine the DVB-NIP broadcast path with unicast
IP delivery to serve receivers without broadcast reception capability or to provide
content not carried on the broadcast multiplex.

### 2.4 Media Over QUIC Transport

Media Over QUIC Transport (MOQT, draft-ietf-moq-transport) is a publish-subscribe
delivery protocol built on QUIC (RFC 9000) and optionally WebTransport for browser
endpoints. MOQT organizes media delivery around a four-level hierarchy:

- **Namespace**: a hierarchical identifier scoping a set of tracks (e.g., a channel or service)
- **Track**: a named, ordered sequence of objects representing a single media stream or catalog
- **Group**: a subsequence of objects that can be independently decoded; typically aligned to a random access point
- **Object**: the atomic unit of delivery, carrying a contiguous payload

Publishers announce tracks and produce objects; subscribers express interest in
tracks and receive objects. MOQT supports partial reliability: publishers assign
delivery priority and expiry to objects, and relays may drop lower-priority or
expired objects without stalling delivery of higher-priority content. This maps
naturally to broadcast loss models where a missed video frame is better discarded
than retransmitted.

MOQT relays cache and forward objects using MOQT namespace, track, group, and
object identifiers. Relays do not parse media payloads, making them
format-agnostic and deployable as general infrastructure between publishers and
subscribers.

### 2.5 MOQT Streaming Format and MSFTS

The MOQT Streaming Format (MSF, draft-ietf-moq-msf) defines a catalog model and
common streaming conventions for tracks delivered over MOQT. The catalog is itself
a MOQT track carrying JSON objects that describe the available media tracks, their
packaging format, codec parameters, and subscription requirements. MSF defines
common track fields including namespace, name, role, MIME type, bitrate, and
alternate group membership.

MSFTS (draft-gregoire-moq-msfts) extends MSF by registering the `"m2ts"`
packaging value for carrying MPEG-2 TS and M2TS source packets over MOQT. When a
track's `packaging` field is `"m2ts"`, additional catalog fields describe the
transport stream structure:

| Field | Type | Description |
|---|---|---|
| `m2tsPacketSize` | Number (required) | Source packet size: 188 (TS) or 192 (M2TS) |
| `m2tsPacketsPerObject` | Number (optional) | Usual number of source packets per MOQT object |
| `m2tsProgramNumber` | Number (optional) | MPEG-2 program number carried by this track |
| `m2tsPmtPid` | Number (optional) | PID of the Program Map Table |
| `m2tsPcrPid` | Number (optional) | PID carrying the Program Clock Reference |
| `m2tsPsiInterval` | Number (optional) | Maximum PAT/PMT repetition interval in milliseconds |
| `m2tsRandomAccess` | Boolean (optional) | When true, each group begins at a random access point |
| `m2tsTimestampMode` | String (optional) | Timestamp semantics for 192-byte packets: `"arrival-time"` or `"opaque"` |
| `m2tsScte35Pid` | Number (optional) | PID carrying SCTE-35 splice signaling |
| `initData` | String (optional) | Base64-encoded initialization source packets (PAT+PMT) |

Each MOQT object payload is a concatenation of whole source packets; the payload
length must be an integer multiple of `m2tsPacketSize`. MOQT group boundaries are
aligned to random access points (IDR frames, or qualifying Clean Random Access
frames). PCR continuity is maintained within each group; a discontinuity between
groups is signaled by the `discontinuity_indicator` bit in the first PCR-carrying
TS packet of the new group.

## 3. Protocol Stack

The following table compares the protocol layers used by DVB-DASH, DVB-NIP, and
MOQ+M2TS across a common set of delivery functions:

| Layer | DVB-DASH | DVB-NIP | MOQ+M2TS |
|---|---|---|---|
| Application | MPEG DASH (MPD + segments) | DVB-I / DVB-DASH | MOQT + MSFTS catalog |
| Media Packaging | ISO BMFF (fragmented MP4) | ISO BMFF via DVB-MABR | M2TS / TS source packets |
| Transport | HTTP/1.1 or HTTP/2 | HTTP/2 over DVB-MABR | QUIC / WebTransport |
| Encapsulation | TCP | GSE (DVB-NIP bearer) | QUIC datagrams or streams |
| Physical | IP network | DVB-S2X, DVB-S2, DVB-T2 | DVB-S2X, DVB-S2, DVB-T2, or IP |

The central architectural property of MOQ+M2TS is that it replaces only the
application and transport layers. The DVB physical bearers (DVB-S2X, DVB-S2,
DVB-T2), GSE encapsulation for broadcast IP delivery, and existing M2TS content
production pipelines — encoders, muxers, conditional access systems, playout
servers — are unchanged. This is the architectural foundation for the
complement, bridge, and replacement analysis presented in Section 6.

### QUIC and WebTransport Integration

MOQT sessions are established over QUIC connections (RFC 9000). For DVB headend
and network operator deployments, MOQT publishers and relays communicate directly
over QUIC. For browser-based subscriber endpoints, WebTransport provides access to
QUIC semantics through a browser API, enabling receivers without native QUIC stacks
to subscribe to MOQT tracks.

In a DVB headend topology, MOQT relays can be deployed at uplink facilities,
regional distribution points, and CDN edge nodes. Relays forward MOQT objects
using only MOQT metadata — namespace, track, group, and object identifiers — without
parsing the M2TS payload. This makes relays format-agnostic and suitable for
deployment as general network infrastructure between a broadcast facility publisher
and geographically distributed subscriber endpoints.

MOQT partial reliability maps to M2TS loss behavior in a way that TCP does not.
When a MOQT object is not delivered — whether due to expiry, priority, or network
loss — the receiving subscriber treats the reconstructed packet stream as
discontinuous at that point and waits for the next random access point before
resuming media presentation. This is consistent with how broadcast receivers
handle TS packet loss: rather than stalling indefinitely waiting for retransmission,
the receiver discards the incomplete access unit and resumes at the next IDR frame.
When `m2tsRandomAccess` is set to true in the MSFTS catalog, every MOQT group
boundary is guaranteed to be a valid recovery point, bounding the maximum
disruption to one group interval regardless of how many objects are missed.

## 4. MSFTS Catalog Integration for DVB Services

### 4.1 Single-Program Satellite Feed

A live satellite contribution feed — for example, a studio-to-headend uplink —
produces 192-octet M2TS source packets. The 4-octet timestamp prefix records the
arrival or emission time of each TS packet, enabling precise STC recovery at
receiving headends without relying solely on PCR values embedded in the stream.

The MSFTS catalog for this feed sets `m2tsPacketSize` to 192 and
`m2tsTimestampMode` to `"arrival-time"`. Setting `m2tsRandomAccess` to true
guarantees that every MOQT group boundary coincides with an IDR frame,
allowing any headend that joins mid-stream to begin decoding at the next group
boundary without scanning for a random access point. The `m2tsPsiInterval`
field declares the maximum PAT/PMT repetition interval in milliseconds; headend
subscribers use this value to estimate how far back they must look to find valid
PSI before their target presentation time. The `initData` field carries a
Base64-encoded sequence of PAT and PMT packets, allowing subscribers to obtain
program structure immediately at join without waiting for the next PSI repetition
cycle.

```json
{
  "version": 1,
  "tracks": [
    {
      "name": "contribution-feed-a",
      "namespace": "uplink.example.dvb/channel/1",
      "packaging": "m2ts",
      "isLive": true,
      "targetLatency": 500,
      "role": "video",
      "mimeType": "video/mp2t",
      "bitrate": 12000000,
      "m2tsPacketSize": 192,
      "m2tsPacketsPerObject": 32,
      "m2tsProgramNumber": 1,
      "m2tsPmtPid": 256,
      "m2tsPcrPid": 257,
      "m2tsPsiInterval": 100,
      "m2tsRandomAccess": true,
      "m2tsTimestampMode": "arrival-time",
      "initData": "<base64-encoded PAT+PMT packets>"
    }
  ]
}

### 4.2 Multi-Program Terrestrial Mux

A regional headend receiving a multi-program transport stream (MPTS) from a
national uplink must filter it into per-program tracks before publishing over
MOQT. MSFTS specifies the filtering rules: each per-program track carries only
the packets belonging to one program — its PAT (rewritten to list only that
program), its PMT, its PCR, and the elementary stream PIDs listed in that PMT.
Null packets (PID 0x1FFF) may be retained or removed at the publisher's
discretion. The `m2tsProgramNumber` field identifies the MPEG-2 program number
carried by the track; `m2tsPmtPid` and `m2tsPcrPid` identify the PMT and PCR
PIDs for that program.

Programs that are independent services — carrying different content — are
published as independent tracks without `altGroup`. Programs that are alternate
renditions of the same content (e.g., the same feed at different bitrates or
language variants) use `altGroup` as described in Section 4.3.

```json
{
  "version": 1,
  "tracks": [
    {
      "name": "service-news",
      "namespace": "headend.example.dvb/mux/regional",
      "packaging": "m2ts",
      "isLive": true,
      "role": "video",
      "mimeType": "video/mp2t",
      "bitrate": 6000000,
      "m2tsPacketSize": 188,
      "m2tsPacketsPerObject": 64,
      "m2tsProgramNumber": 1,
      "m2tsPmtPid": 256,
      "m2tsPcrPid": 257,
      "m2tsPsiInterval": 100,
      "m2tsRandomAccess": true
    },
    {
      "name": "service-sports",
      "namespace": "headend.example.dvb/mux/regional",
      "packaging": "m2ts",
      "isLive": true,
      "role": "video",
      "mimeType": "video/mp2t",
      "bitrate": 8000000,
      "m2tsPacketSize": 188,
      "m2tsPacketsPerObject": 64,
      "m2tsProgramNumber": 2,
      "m2tsPmtPid": 512,
      "m2tsPcrPid": 513,
      "m2tsPsiInterval": 100,
      "m2tsRandomAccess": true
    }
  ]
}

### 4.3 ABR Alternate Renditions

When the same content is available at multiple bitrates — for example, a live
channel encoded at 8 Mbit/s and 4 Mbit/s — the MSFTS `altGroup` field links the
tracks as alternate renditions. Subscribers may switch between tracks in an
alternate group to adapt to available bandwidth.

MSFTS imposes two requirements on alternate rendition tracks. First, Group
boundaries must be aligned at identical presentation positions across all tracks
in the group. Because each group begins at an IDR frame (when `m2tsRandomAccess`
is true), this means IDR frames at the same presentation time across renditions.
Second, after every track switch, the subscriber must treat the transition as a
PCR discontinuity and reinitialize its STC from the first PCR value received on
the new track. Additionally, because PID assignments are not required to match
across alternate tracks, the subscriber must re-parse the PAT and PMT of the new
track before routing elementary-stream packets to a decoder.

```json
{
  "version": 1,
  "tracks": [
    {
      "name": "video-high",
      "namespace": "headend.example.dvb/channel/1",
      "packaging": "m2ts",
      "isLive": true,
      "role": "video",
      "mimeType": "video/mp2t",
      "bitrate": 8000000,
      "altGroup": 1,
      "m2tsPacketSize": 188,
      "m2tsPacketsPerObject": 64,
      "m2tsProgramNumber": 1,
      "m2tsPmtPid": 256,
      "m2tsPcrPid": 257,
      "m2tsPsiInterval": 100,
      "m2tsRandomAccess": true
    },
    {
      "name": "video-low",
      "namespace": "headend.example.dvb/channel/1",
      "packaging": "m2ts",
      "isLive": true,
      "role": "video",
      "mimeType": "video/mp2t",
      "bitrate": 4000000,
      "altGroup": 1,
      "m2tsPacketSize": 188,
      "m2tsPacketsPerObject": 64,
      "m2tsProgramNumber": 1,
      "m2tsPmtPid": 512,
      "m2tsPcrPid": 513,
      "m2tsPsiInterval": 100,
      "m2tsRandomAccess": true
    }
  ]
}

### 4.4 SCTE-35 and Splice Signaling

SCTE-35 splice signaling is carried transparently in the MPEG-2 Transport Stream
as `splice_info_section()` messages on a PID registered in the PMT. MSFTS does
not alter or process SCTE-35 messages; they pass through MOQT objects as part of
the source packet stream, opaque to relays.

The `m2tsScte35Pid` catalog field is advisory: it allows subscribers to locate
splice events by PID without parsing the PMT. Publishers that carry SCTE-35
signaling should include this field. In DVB-DASH deployments, SCTE-35 events are
often also surfaced as MPEG-DASH event streams in the manifest. Publishers
integrating MOQ+M2TS alongside DVB-DASH may optionally surface splice events via
the MSF Event Timeline mechanism defined in MSF; this document does not specify
SCTE-35 processing behavior.

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

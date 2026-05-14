# MOQ+DVB+M2TS Whitepaper Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Write a self-contained technical whitepaper describing how MOQT carrying MPEG-2 TS/M2TS-packaged tracks via the MSFTS extension integrates with DVB-S2/S2X, DVB-T2, and hybrid broadcast-broadband infrastructure, with a dual call to action for DVB and IETF standardization.

**Architecture:** Single Markdown document organized as a standards layering whitepaper: background primer → protocol stack → catalog integration → deployment scenarios → standards relationship → standardization path. The complement/bridge/replace arc runs through sections 6-7 as analysis, not upfront argument. Each section is independently committable.

**Tech Stack:** Markdown (CommonMark). Source file at `moq-dvb-m2ts-whitepaper.md`. Design spec at `docs/superpowers/specs/2026-05-14-moq-dvb-m2ts-whitepaper-design.md`.

---

## File Structure

| File | Purpose |
|---|---|
| `moq-dvb-m2ts-whitepaper.md` | The whitepaper document — all sections written here incrementally |
| `docs/superpowers/specs/2026-05-14-moq-dvb-m2ts-whitepaper-design.md` | Reference spec — consult before writing each section |
| `docs/superpowers/plans/2026-05-14-moq-dvb-m2ts-whitepaper.md` | This plan |

---

### Task 1: Scaffold document with title, abstract, and section stubs

**Files:**
- Create: `moq-dvb-m2ts-whitepaper.md`

- [ ] **Step 1: Create the document scaffold**

Create `moq-dvb-m2ts-whitepaper.md` with the following content exactly:

```markdown
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

<!-- TODO: Task 2 -->

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
```

- [ ] **Step 2: Verify file was created and scaffold is complete**

```bash
grep -c "^##" moq-dvb-m2ts-whitepaper.md
```

Expected output: `10` (9 top-level sections + Abstract rendered as ##)

- [ ] **Step 3: Commit scaffold**

```bash
git add moq-dvb-m2ts-whitepaper.md
git commit -m "docs: scaffold MOQ+DVB+M2TS whitepaper with title, abstract, and section stubs"
```

---

### Task 2: Write Section 1 — Introduction

**Files:**
- Modify: `moq-dvb-m2ts-whitepaper.md` (Section 1)

**Content requirements from design spec:**
- Frame the problem: DVB-DASH and DVB-NIP both assume HTTP/TCP at application transport layer
- Name the specific limitations: TCP head-of-line blocking, HTTP request-response semantics
- Introduce MOQT as the solution: multiplexed, partially-reliable, object-oriented delivery over QUIC
- State the paper's dual purpose: (1) describe how MOQT+M2TS integrates with DVB infrastructure, (2) articulate the standardization opportunity for DVB and IETF
- Target length: ~400 words

- [ ] **Step 1: Replace the Section 1 stub with the full introduction prose**

Replace `<!-- TODO: Task 2 -->` under `## 1. Introduction` with:

```markdown
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
```

- [ ] **Step 2: Check word count of Section 1**

```bash
awk '/^## 1\. Introduction/,/^## 2\. Background/' moq-dvb-m2ts-whitepaper.md | wc -w
```

Expected: 350-450 words.

- [ ] **Step 3: Commit**

```bash
git add moq-dvb-m2ts-whitepaper.md
git commit -m "docs: write Section 1 Introduction for MOQ+DVB+M2TS whitepaper"
```

---

### Task 3: Write Section 2 — Background (all five subsections)

**Files:**
- Modify: `moq-dvb-m2ts-whitepaper.md` (Section 2)

**Content requirements from design spec:**
- 2.1: 188-byte TS packets, 192-byte M2TS with 4-byte timestamp, PAT/PMT/PCR/PTS/DTS, SCTE-35, SPTS vs MPTS — self-contained for new readers
- 2.2: DVB-DASH = MPEG DASH + ISO BMFF + HTTP ABR; codec toolkit (AVC/HEVC/VVC, HE-AAC, AC-4); DVB-I service discovery
- 2.3: DVB-NIP = GSE encapsulation over S2X/S2/T2; DVB-MABR multicast ABR; hybrid broadcast+broadband
- 2.4: QUIC, MOQT object model (namespace/track/group/object), partial reliability, relay architecture, pub/sub roles
- 2.5: MSF catalog model, `"m2ts"` packaging value, key fields, object payload structure, group numbering at random access points
- Target length: ~800 words total across five subsections

- [ ] **Step 1: Replace the five Background stubs with prose**

Replace each `<!-- TODO: Task 3 -->` under sections 2.1–2.5 with the following content for each subsection:

**2.1 — replace stub with:**

```markdown
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
```

**2.2 — replace stub with:**

```markdown
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
```

**2.3 — replace stub with:**

```markdown
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
```

**2.4 — replace stub with:**

```markdown
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
```

**2.5 — replace stub with:**

```markdown
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
```

- [ ] **Step 2: Verify all five subsection stubs are replaced**

```bash
grep -c "TODO: Task 3" moq-dvb-m2ts-whitepaper.md
```

Expected output: `0`

- [ ] **Step 3: Commit**

```bash
git add moq-dvb-m2ts-whitepaper.md
git commit -m "docs: write Section 2 Background for MOQ+DVB+M2TS whitepaper"
```

---

### Task 4: Write Section 3 — Protocol Stack

**Files:**
- Modify: `moq-dvb-m2ts-whitepaper.md` (Section 3)

**Content requirements from design spec:**
- Layer comparison table: DVB-DASH vs DVB-NIP vs MOQ+M2TS across Application / Media Packaging / Transport / Encapsulation / Physical
- Central claim: MOQ+M2TS replaces only the application and transport layers; physical bearers, GSE, and M2TS production pipelines are preserved
- QUIC/WebTransport integration: session establishment, relay topology in DVB headend/CDN, partial reliability vs M2TS loss behavior
- Target length: ~500 words

- [ ] **Step 1: Replace the Section 3 stub with the full protocol stack content**

Replace `<!-- TODO: Task 4 -->` under `## 3. Protocol Stack` with:

```markdown
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
```

- [ ] **Step 2: Verify the table and stub replacement**

```bash
grep -c "TODO: Task 4" moq-dvb-m2ts-whitepaper.md
```

Expected output: `0`

- [ ] **Step 3: Commit**

```bash
git add moq-dvb-m2ts-whitepaper.md
git commit -m "docs: write Section 3 Protocol Stack for MOQ+DVB+M2TS whitepaper"
```

---

### Task 5: Write Section 4 — MSFTS Catalog Integration for DVB Services

**Files:**
- Modify: `moq-dvb-m2ts-whitepaper.md` (Section 4)

**Content requirements from design spec:**
- 4.1: Single-program satellite feed — `m2tsPacketSize: 192`, `m2tsTimestampMode: "arrival-time"`, `m2tsRandomAccess: true`, `m2tsPsiInterval`, `initData` for fast join; explain each field in DVB operator terms
- 4.2: Multi-program terrestrial mux — MPTS filtering, separate tracks per program, PAT rewriting, `m2tsProgramNumber`, `m2tsPmtPid`, `m2tsPcrPid`, null packet handling, independent programs (no `altGroup`)
- 4.3: ABR alternate renditions — `altGroup`, Group boundary alignment at IDR, PCR discontinuity on track switch, PAT/PMT re-parse requirement, PID assignments need not match
- 4.4: SCTE-35 — `m2tsScte35Pid` advisory field, transparent carriage, relationship to DVB-DASH event stream signaling
- Include JSON catalog examples for each subsection

- [ ] **Step 1: Replace the four Section 4 stubs with prose and catalog JSON**

Replace `<!-- TODO: Task 5 -->` under section 4.1 with:

```markdown
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
```
```

Replace `<!-- TODO: Task 5 -->` under section 4.2 with:

```markdown
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
```
```

Replace `<!-- TODO: Task 5 -->` under section 4.3 with:

```markdown
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
```
```

Replace `<!-- TODO: Task 5 -->` under section 4.4 with:

```markdown
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
```

- [ ] **Step 2: Verify all Section 4 stubs are replaced**

```bash
grep -c "TODO: Task 5" moq-dvb-m2ts-whitepaper.md
```

Expected output: `0`

- [ ] **Step 3: Commit**

```bash
git add moq-dvb-m2ts-whitepaper.md
git commit -m "docs: write Section 4 MSFTS Catalog Integration for MOQ+DVB+M2TS whitepaper"
```

---

### Task 6: Write Section 5 — DVB Deployment Scenarios

**Files:**
- Modify: `moq-dvb-m2ts-whitepaper.md` (Section 5)

**Content requirements from design spec:**
- Each scenario: topology → signal flow → MSFTS catalog configuration → key operational considerations
- 5.1 Satellite: contribution feed, 192-byte M2TS, MOQT publisher at uplink, headends subscribe over S2X, PCR continuity, `initData` for fast join
- 5.2 Terrestrial: MPTS at regional headend, MOQT publisher filters to per-program tracks, T2 transmitters subscribe and reconstruct MPTS, `m2tsPsiInterval` bounds join latency
- 5.3 Hybrid: DVB-NIP satellite multicast + MOQT unicast; relay bridges broadcast to QUIC; `altGroup` for satellite/unicast renditions; Group boundary and PTS alignment requirements
- Target length: ~900 words total

- [ ] **Step 1: Replace the three Section 5 stubs with full scenario prose**

Replace `<!-- TODO: Task 6 -->` under section 5.1 with:

```markdown
**Topology:** A broadcast facility encodes a live event as a single-program
transport stream at contribution quality and outputs 192-byte M2TS source packets.
A MOQT publisher process at the uplink facility ingests the M2TS output and
publishes it as a MOQT track with `m2tsPacketSize: 192` and
`m2tsTimestampMode: "arrival-time"`. A MOQT relay co-located with the satellite
uplink accepts the published track and makes it available to downstream
subscribers.

**Signal flow:** The relay forwards MOQT objects to DVB headend subscribers over
QUIC, with the QUIC connection carried over IP encapsulated in GSE on the DVB-S2X
bearer. Each headend subscribes to the contribution track, receives MOQT objects,
reconstructs the 192-byte M2TS packet stream from the object payloads in group and
object ID order, and passes the stream to its downstream processing chain.

**MSFTS catalog configuration:** The catalog declares `m2tsRandomAccess: true`,
guaranteeing that every MOQT group begins at an IDR frame together with the PAT
and PMT packets required for program demultiplexing. The `m2tsPsiInterval` value
bounds the maximum interval between PAT/PMT repetitions; headends use this to
estimate maximum join latency. The `initData` field carries Base64-encoded PAT
and PMT packets, enabling a joining headend to obtain program structure immediately
without waiting for the next PSI repetition in the stream.

**Key operational considerations:** PCR continuity is maintained within each MOQT
group. A PCR discontinuity introduced between groups — for example, at a production
cut — is signaled by the `discontinuity_indicator` bit in the adaptation field of
the first PCR-carrying TS packet in the new group, following MPEG-2 TS conventions.
The 4-octet M2TS arrival timestamp enables receiving headends to recover STC with
precision beyond what PCR alone provides, which is significant for contribution
feeds that feed into downstream encoding or record systems with tight timing
requirements. Conditional access and scrambling information present in the
transport stream passes through MOQT objects unchanged; MOQT relays do not parse
or modify TS payloads.
```

Replace `<!-- TODO: Task 6 -->` under section 5.2 with:

```markdown
**Topology:** A regional headend receives an MPTS from a national uplink
containing multiple program services. It must deliver each service to the
DVB-T2 transmitter network that serves its coverage area. The headend runs a
MOQT publisher that ingests the MPTS and publishes one MOQT track per program
service using 188-byte TS packets. Each transmitter site runs a MOQT subscriber
that selects the program tracks it is licensed to transmit and reconstructs a
local MPTS for over-the-air emission.

**Signal flow:** The regional headend publisher filters the incoming MPTS according
to MSFTS multi-program handling rules: for each program, it retains only the
packets belonging to that program (PAT rewritten to list one program, PMT, PCR PID,
and all elementary stream PIDs listed in the PMT) and publishes them as a separate
MOQT track. Each DVB-T2 transmitter site subscribes to the tracks it requires and
appends received source packets in MOQT object order to reconstruct the packet
stream. The transmitter then combines the per-program streams into a local MPTS for
modulation and transmission on the DVB-T2 bearer.

**MSFTS catalog configuration:** Each per-program track includes `m2tsProgramNumber`,
`m2tsPmtPid`, and `m2tsPcrPid` so that transmitter subscribers can identify program
structure without parsing PSI. The `m2tsPsiInterval` value tells each transmitter
site the maximum interval between PAT and PMT repetitions. When a transmitter
subscriber joins an active track, it must not begin transmission until it has
received a valid PAT and PMT for the program; `m2tsPsiInterval` bounds how long it
must wait before a valid PSI cycle is guaranteed to have been received.

**Key operational considerations:** PAT rewriting at the publisher is required by
the MSFTS specification: each per-program track must carry a PAT listing only the
program present in that track. Transmitter sites that reconstruct a multi-program
MPTS from multiple MOQT tracks must produce a new combined PAT for the local
multiplex. Null packet handling — whether to strip null packets from individual
program tracks or retain them — is a publisher policy decision; transmitters
generating a local MPTS may need to add null packets to fill the fixed-bitrate
DVB-T2 transport capacity.
```

Replace `<!-- TODO: Task 6 -->` under section 5.3 with:

```markdown
**Topology:** A service provider delivers a live channel via DVB-NIP satellite
multicast (DVB-MABR over DVB-S2X) for receivers with satellite capability and via
MOQT unicast over QUIC for broadband-only devices or devices outside the satellite
footprint. A MOQT relay bridges the two delivery paths: it ingests the channel
from the DVB-NIP broadcast feed and republishes it as MOQT tracks accessible over
QUIC. Both delivery paths carry the same M2TS-packaged content.

**Signal flow:** Satellite-capable receivers subscribe via DVB-MABR and receive
ISO BMFF-segmented content via DVB-DASH as specified in DVB-NIP. Broadband
receivers connect to the MOQT relay over QUIC and subscribe to the M2TS-packaged
MOQT track. The relay ingests from the broadcast feed, produces MOQT objects at
group boundaries aligned to IDR frames, and forwards them to unicast subscribers.
When both broadcast and unicast renditions of the same content are available at
different bitrates, the MSFTS `altGroup` field links them so that subscribers aware
of both paths can select the appropriate rendition.

**MSFTS catalog configuration:** Tracks representing the satellite broadcast
rendition and MOQT unicast renditions of the same channel are assigned the same
`altGroup` value if they carry the same content. Video tracks in the alternate
group must align Group boundaries at identical presentation timestamps, enabling a
subscriber to switch between broadcast and unicast delivery at group boundaries
without presentation discontinuity. Publishers providing alternate tracks must
align PTS values at Group boundaries across tracks to enable seamless switching at
the application layer.

**Key operational considerations:** A subscriber switching between alternate tracks
must treat the transition as a PCR discontinuity and reinitialize STC recovery
from the first PCR on the new track. It must also re-parse PAT and PMT after the
switch because PID assignments need not match between the satellite and unicast
renditions. The MOQT relay does not parse DVB-MABR or ISO BMFF; it ingests at the
M2TS packet level. The relay's MOQT cache policy determines how many groups are
retained for late-joining subscribers; when `m2tsRandomAccess` is true, the relay
should retain at minimum the first object of each cached group, as that object
contains the IDR frame and PSI needed by joining subscribers.
```

- [ ] **Step 2: Verify all Section 5 stubs are replaced**

```bash
grep -c "TODO: Task 6" moq-dvb-m2ts-whitepaper.md
```

Expected output: `0`

- [ ] **Step 3: Commit**

```bash
git add moq-dvb-m2ts-whitepaper.md
git commit -m "docs: write Section 5 DVB Deployment Scenarios for MOQ+DVB+M2TS whitepaper"
```

---

### Task 7: Write Section 6 — Relationship to Existing DVB Standards

**Files:**
- Modify: `moq-dvb-m2ts-whitepaper.md` (Section 6)

**Content requirements from design spec:**
- 6.1 Complement: no changes to physical layers, GSE, DVB-I, codec profiles, or content protection; scrambling opaque to MOQT relays; deploy alongside DVB-DASH for low-latency/contribution cases
- 6.2 Bridge: M2TS production workflows unchanged; MSFTS maps existing packet stream directly; key advantage vs DVB-DASH is no ISO BMFF re-wrapping required; `initData` and PSI rules carry existing DVB service information without modification
- 6.3 Replacement Path: greenfield IP-only or next-gen DVB profiles; QUIC replaces HTTP/TCP; M2TS retained; partial reliability maps to broadcast loss tolerance; MOQT relay caching replaces HTTP CDN infrastructure
- Target length: ~600 words

- [ ] **Step 1: Replace the three Section 6 stubs with prose**

Replace `<!-- TODO: Task 7 -->` under section 6.1 with:

```markdown
MOQ+M2TS does not require changes to any layer of the DVB stack below the
application transport. DVB physical layers (DVB-S2, DVB-S2X, DVB-T2), GSE
encapsulation, DVB-I service discovery, DVB codec profiles (AVC, HEVC, VVC,
HE-AAC, AC-4), and content protection mechanisms are unaffected. Transport-stream
scrambling and conditional access information are carried inside TS packets and are
opaque to MOQT relays, which forward objects without inspecting payloads.

Operators can deploy MOQT as an additional transport path for use cases where
DVB-DASH's HTTP/TCP characteristics are limiting — contribution links where
head-of-line blocking adds latency, or low-latency distribution scenarios. The
MOQT path and the DVB-DASH path can coexist, fed from the same M2TS production
workflow, serving different receiver populations or use cases. No existing
DVB-DASH or DVB-NIP infrastructure needs to be removed or modified to introduce
MOQT.
```

Replace `<!-- TODO: Task 7 -->` under section 6.2 with:

```markdown
The most operationally significant property of MSFTS for existing DVB deployments
is that it requires no re-packaging of M2TS content. DVB-DASH requires elementary
streams to be re-wrapped in ISO BMFF fragmented MP4 containers, which introduces
an encoding boundary: content must pass through an ISO BMFF packager before it can
be delivered. This packager adds latency, complexity, and a point of failure in
the contribution or distribution chain.

MSFTS eliminates this boundary. The publisher reads 188-byte or 192-byte source
packets directly from the M2TS output of an existing encoder or muxer and writes
them into MOQT object payloads. Encoders, muxers, playout systems, conditional
access headends, and other equipment that already produce M2TS output require no
modification. The MSFTS catalog fields — `m2tsProgramNumber`, `m2tsPmtPid`,
`m2tsPcrPid`, `m2tsPsiInterval` — describe the program structure already present
in the transport stream. The `initData` field carries PAT and PMT packets extracted
from the live stream with no transformation. The existing DVB service information
architecture is preserved in its entirety.

This makes MOQ+M2TS a natural migration bridge: operators can introduce MOQT as
an output path from their existing M2TS infrastructure, serve a new population of
MOQT-capable receivers, and evaluate the technology without committing to a
re-architecture of their production chain.
```

Replace `<!-- TODO: Task 7 -->` under section 6.3 with:

```markdown
For greenfield IP-only deployments — for example, a next-generation contribution
network built on QUIC rather than TCP, or a future DVB IP profile that specifies
MOQT as a delivery layer — MOQ+M2TS provides a unified transport for both
contribution and distribution. In this scenario, MOQT replaces the HTTP/TCP stack
of DVB-DASH across the entire delivery chain, from the encoder output to the
receiver, while M2TS is retained as the media container. No other DVB technology
changes.

MOQT partial reliability maps to broadcast loss tolerance more naturally than TCP
retransmission. In a broadcast environment, a decoder that misses a video access
unit discards it and waits for the next IDR frame rather than stalling the
presentation. MOQT's object expiry and priority mechanisms allow a publisher to
express this behavior explicitly: lower-priority or time-expired objects may be
dropped by relays without blocking delivery of subsequent content. TCP retransmits
every byte, making it incompatible with this loss model except through application-layer
workarounds.

MOQT relay caching provides CDN-like distribution without requiring HTTP
infrastructure. Relays retain MOQT groups according to cache policy and serve
late-joining subscribers from cache, performing a function analogous to an HTTP
CDN origin cache but operating on MOQT objects rather than HTTP segments. For DVB
operators, this represents an opportunity to reduce dependency on HTTP CDN
infrastructure for IP-delivered services while retaining the distribution
efficiency that CDN caching provides.
```

- [ ] **Step 2: Verify all Section 6 stubs are replaced**

```bash
grep -c "TODO: Task 7" moq-dvb-m2ts-whitepaper.md
```

Expected output: `0`

- [ ] **Step 3: Commit**

```bash
git add moq-dvb-m2ts-whitepaper.md
git commit -m "docs: write Section 6 Relationship to DVB Standards for MOQ+DVB+M2TS whitepaper"
```

---

### Task 8: Write Section 7 — Standardization Path

**Files:**
- Modify: `moq-dvb-m2ts-whitepaper.md` (Section 7)

**Content requirements from design spec:**
- 7.1 IETF: MSFTS is informational extension to MSF; DVB scenarios = concrete real-world applicability evidence; two areas for future MSFTS revision (PSI repetition rate signaling in contribution feeds; relay behavior for hybrid broadcast-broadband)
- 7.2 DVB: MOQ+M2TS as candidate DVB profile analogous to DVB-DASH; proposed study mission scope (codec/bitrate constraints, PSI requirements, DVB-I integration, DVB-NIP interoperability); call to DVB members to evaluate and report
- Target length: ~400 words

- [ ] **Step 1: Replace the two Section 7 stubs with prose**

Replace `<!-- TODO: Task 8 -->` under section 7.1 with:

```markdown
The MSFTS draft (`draft-gregoire-moq-msfts`) is submitted to the IETF MOQ Working
Group as an informational document extending the MOQT Streaming Format
(`draft-ietf-moq-msf`). The DVB deployment scenarios described in this paper
constitute concrete evidence of real-world applicability: they demonstrate that
the `"m2ts"` packaging value and its associated catalog fields are sufficient to
describe the service structures, timing requirements, and operational constraints
of DVB satellite contribution, terrestrial distribution, and hybrid
broadcast-broadband delivery.

Two areas of DVB practice may inform future revisions of MSFTS. First, PSI
repetition rate signaling: the `m2tsPsiInterval` field currently declares the
maximum interval between PAT/PMT repetitions, but DVB contribution feeds often
use specific repetition patterns governed by headend equipment configuration.
Finer-grained PSI signaling — for example, separate intervals for PAT and PMT,
or minimum as well as maximum intervals — may be worth specifying as DVB
deployment experience accumulates. Second, relay behavior for hybrid
broadcast-broadband topologies: the interaction between DVB-MABR multicast
delivery and MOQT unicast relay caching involves relay state and cache policy
decisions that are not fully addressed in the current MSFTS or MSF
specifications. Operational experience from hybrid deployments would inform
whether additional relay guidance is needed.

MOQ Working Group participants with DVB expertise or deployment access are
invited to contribute findings to the working group.
```

Replace `<!-- TODO: Task 8 -->` under section 7.2 with:

```markdown
MOQ+M2TS is a candidate profile for a future DVB specification, analogous in
structure to DVB-DASH: a constrained profile of MOQT, MSF, and MSFTS tailored to
DVB service delivery requirements. Such a profile would specify the subset of
MOQT and MSFTS options applicable to DVB services and add DVB-specific constraints
where needed.

A DVB study mission or technical module addressing MOQ+M2TS would productively
scope the following areas:

- **Codec and bitrate constraints**: which DVB codec profiles (AVC, HEVC, VVC,
  HE-AAC, AC-4, subtitles) and service bitrate ranges are in scope for
  MOQ+M2TS delivery, and whether additional catalog fields are needed to describe
  them.
- **PSI repetition requirements**: mandatory minimum PAT/PMT repetition intervals
  for live contribution and distribution use cases, expressed in terms of
  `m2tsPsiInterval` or additional fields.
- **DVB-I service discovery integration**: how MOQT-delivered services are
  described in DVB-I service lists, including the mapping from DVB-I service
  records to MOQT namespace and track identifiers.
- **DVB-NIP interoperability**: requirements for relay and subscriber behavior
  when MOQT delivery coexists with DVB-NIP/DVB-MABR delivery of the same
  service.

DVB member organizations — broadcasters, equipment vendors, conditional access
providers, and network operators — are invited to evaluate MOQ+M2TS in their
deployment contexts and to contribute findings to both DVB and the IETF MOQ
Working Group. The MSFTS draft is openly available for review and comment.
```

- [ ] **Step 2: Verify both Section 7 stubs are replaced**

```bash
grep -c "TODO: Task 8" moq-dvb-m2ts-whitepaper.md
```

Expected output: `0`

- [ ] **Step 3: Commit**

```bash
git add moq-dvb-m2ts-whitepaper.md
git commit -m "docs: write Section 7 Standardization Path for MOQ+DVB+M2TS whitepaper"
```

---

### Task 9: Write Section 8 — Conclusion

**Files:**
- Modify: `moq-dvb-m2ts-whitepaper.md` (Section 8)

**Content requirements from design spec:**
- Restate the three-part argument: complement (no infrastructure disruption), bridge (no re-encoding), replacement path (QUIC replaces HTTP/TCP)
- Name MSFTS as the technical foundation
- Close with invitation to both DVB members and IETF MOQ WG participants
- Target length: ~200 words

- [ ] **Step 1: Replace the Section 8 stub with the conclusion prose**

Replace `<!-- TODO: Task 9 -->` under `## 8. Conclusion` with:

```markdown
This paper has presented a three-part architectural argument for MOQ+M2TS in DVB
deployments.

As a complement to existing infrastructure, MOQ+M2TS requires no changes to DVB
physical layers, GSE encapsulation, service discovery, codec profiles, or content
protection. It can be deployed alongside DVB-DASH and DVB-NIP for specific use
cases without displacing any existing investment.

As a migration bridge, MSFTS enables M2TS source packets to be carried over MOQT
without re-encoding or re-packaging. Existing encoders, muxers, and playout
systems require no modification. DVB service information — PAT, PMT, PCR, SCTE-35
— is preserved in the transport stream and described in the MSFTS catalog. The
encoding boundary imposed by ISO BMFF re-wrapping in DVB-DASH is eliminated.

As a replacement path for greenfield or next-generation deployments, MOQ+M2TS
replaces the HTTP/TCP transport stack with QUIC while retaining M2TS as the media
container. MOQT partial reliability aligns with broadcast loss tolerance; MOQT
relay caching provides CDN-equivalent distribution without HTTP infrastructure.

The MSFTS extension to the MOQT Streaming Format is the technical foundation
making this trajectory possible. DVB member organizations and IETF MOQ Working
Group participants are invited to engage with the MSFTS draft and to contribute
deployment experience that will inform its development and the evolution of DVB IP
transport standards.
```

- [ ] **Step 2: Verify stub is replaced**

```bash
grep -c "TODO: Task 9" moq-dvb-m2ts-whitepaper.md
```

Expected output: `0`

- [ ] **Step 3: Commit**

```bash
git add moq-dvb-m2ts-whitepaper.md
git commit -m "docs: write Section 8 Conclusion for MOQ+DVB+M2TS whitepaper"
```

---

### Task 10: Write Section 9 — References

**Files:**
- Modify: `moq-dvb-m2ts-whitepaper.md` (Section 9)

**Content requirements from design spec:**
- Normative: ISO/IEC 13818-1, draft-ietf-moq-transport, draft-ietf-moq-msf, draft-gregoire-moq-msfts, ETSI EN 303 560, ETSI EN 303 285, ETSI EN 302 307, ETSI EN 302 307-2, ETSI EN 302 755, RFC 9000
- Informative: ETSI TS 103 770, ETSI TS 103 769, SCTE-35, draft-ietf-moq-secure-objects, draft-ietf-moq-c4m, draft-ietf-moq-privacy-pass-auth

- [ ] **Step 1: Replace the Section 9 stub with the references**

Replace `<!-- TODO: Task 10 -->` under `## 9. References` with:

```markdown
### Normative References

- **ISO/IEC 13818-1** — Information technology — Generic coding of moving pictures
  and associated audio information: Systems. ISO/IEC, 2023.

- **RFC 9000** — QUIC: A UDP-Based Multiplexed and Secure Transport. Iyengar, J.
  and M. Thomson (Eds.), IETF, 2021.

- **draft-ietf-moq-transport** — Media Over QUIC Transport. IETF MOQ Working
  Group. (Work in progress.)

- **draft-ietf-moq-msf** — MOQT Streaming Format. IETF MOQ Working Group. (Work
  in progress.)

- **draft-gregoire-moq-msfts** — MPEG-2 Transport Stream Packaging for Media Over
  QUIC Transport. Gregoire, P. and G. Simon. (Work in progress.)
  https://mondain.github.io/msfts/draft-gregoire-moq-msfts.html

- **ETSI EN 303 285** — Digital Video Broadcasting (DVB); MPEG-DASH Profile for
  Transport of ISO BMFF Based DVB Services over IP Based Networks. ETSI.

- **ETSI EN 303 560** — Digital Video Broadcasting (DVB); Native IP Broadcasting.
  ETSI.

- **ETSI EN 302 307** — Digital Video Broadcasting (DVB); Second generation
  framing structure, channel coding and modulation systems for Broadcasting,
  Interactive Services, News Gathering and other broadband satellite applications
  (DVB-S2). ETSI.

- **ETSI EN 302 307-2** — Digital Video Broadcasting (DVB); Second Generation
  Extensions to the Second Generation (DVB-S2X). ETSI.

- **ETSI EN 302 755** — Digital Video Broadcasting (DVB); Frame structure channel
  coding and modulation for a second generation digital terrestrial television
  broadcasting system (DVB-T2). ETSI.

### Informative References

- **ETSI TS 103 770** — Digital Video Broadcasting (DVB); DVB-I Specification.
  ETSI.

- **ETSI TS 103 769** — Digital Video Broadcasting (DVB); Multicast ABR
  Delivery (DVB-MABR). ETSI.

- **SCTE-35** — Digital Program Insertion Cueing Message. Society of Cable
  Telecommunications Engineers.

- **draft-ietf-moq-secure-objects** — Secure Objects for Media Over QUIC. IETF
  MOQ Working Group. (Work in progress.)

- **draft-ietf-moq-c4m** — Common Access Token for Media Over QUIC. IETF MOQ
  Working Group. (Work in progress.)

- **draft-ietf-moq-privacy-pass-auth** — Privacy Pass Authorization for Media
  Over QUIC. IETF MOQ Working Group. (Work in progress.)
```

- [ ] **Step 2: Verify stub is replaced and no TODO comments remain**

```bash
grep -c "TODO" moq-dvb-m2ts-whitepaper.md
```

Expected output: `0`

- [ ] **Step 3: Final commit**

```bash
git add moq-dvb-m2ts-whitepaper.md
git commit -m "docs: write Section 9 References and complete MOQ+DVB+M2TS whitepaper"
```

---

## Plan Self-Review

### Spec Coverage

| Spec requirement | Task |
|---|---|
| Title and abstract | Task 1 |
| Self-contained background (TS/M2TS, DVB-DASH, DVB-NIP, MOQT, MSF/MSFTS) | Task 3 |
| Protocol stack comparison table | Task 4 |
| QUIC/WebTransport integration and relay topology | Task 4 |
| Partial reliability vs broadcast loss model | Task 4 |
| Satellite feed catalog example (192-byte, initData, m2tsTimestampMode) | Task 5 |
| Multi-program terrestrial catalog example (MPTS filtering, per-program tracks) | Task 5 |
| ABR alternate renditions (altGroup, Group alignment, PCR discontinuity, PAT/PMT re-parse) | Task 5 |
| SCTE-35 advisory field and transparent carriage | Task 5 |
| Satellite contribution scenario (topology, signal flow, operational notes) | Task 6 |
| Terrestrial distribution scenario (MPTS filtering at headend, T2 transmitter reconstruction) | Task 6 |
| Hybrid broadcast-broadband scenario (DVB-NIP + QUIC unicast, relay bridge, altGroup) | Task 6 |
| Complement analysis | Task 7 |
| Bridge analysis (no ISO BMFF re-wrapping required) | Task 7 |
| Replacement path analysis (QUIC vs HTTP/TCP, relay caching vs CDN) | Task 7 |
| IETF standardization path (MSFTS applicability evidence, two revision areas) | Task 8 |
| DVB standardization path (study mission scope: codecs, PSI, DVB-I, DVB-NIP) | Task 8 |
| Conclusion restating three-part argument | Task 9 |
| Normative and informative references | Task 10 |
| No implementation or vendor specifics | All tasks — no implementation content anywhere |
| Dual audience served | Introduction (Task 2) explicitly states both audiences |

All spec requirements covered.

### Placeholder Scan

No TBDs, TODOs (in final document), or vague requirements in any task. Every step includes exact file paths, exact commands with expected output, and complete prose content for each section.

### Type Consistency

No code types to check. All MSFTS field names (`m2tsPacketSize`, `m2tsRandomAccess`, `m2tsTimestampMode`, `m2tsPsiInterval`, `m2tsProgramNumber`, `m2tsPmtPid`, `m2tsPcrPid`, `m2tsScte35Pid`, `initData`, `altGroup`) are used consistently across Tasks 3, 5, 6, and 7, matching the MSFTS draft exactly. Draft identifiers are consistent throughout (`draft-gregoire-moq-msfts`, `draft-ietf-moq-transport`, `draft-ietf-moq-msf`).
```

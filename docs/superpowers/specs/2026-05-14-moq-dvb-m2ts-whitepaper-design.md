---
name: moq-dvb-m2ts-whitepaper-design
description: Design spec for whitepaper on Media Over QUIC Transport for DVB services using MPEG-2 TS/M2TS packaging via the MSFTS draft
metadata:
  type: project
---

# Whitepaper Design: Media Over QUIC Transport for DVB Services Using MPEG-2 Transport Stream Packaging

## Title and Abstract

**Title:** Media Over QUIC Transport for DVB Services Using MPEG-2 Transport Stream Packaging

**Subtitle:** A Technical Whitepaper on Deploying MOQ+M2TS Across DVB Satellite and Terrestrial Networks

**Abstract:** This whitepaper describes an architectural framework for carrying DVB services over Media Over QUIC Transport (MOQT) using MPEG-2 Transport Stream and M2TS source packets, as defined by the MSFTS packaging extension to the MOQT Streaming Format (MSF). It covers the protocol stack integration with DVB-S2/S2X, DVB-T2, and hybrid broadcast-broadband infrastructures; the role of MSFTS catalog fields in describing DVB service tracks; and three deployment scenarios spanning broadcast contribution, multicast distribution, and unicast streaming. The paper analyses how MOQ+M2TS complements existing DVB-DASH and DVB-NIP deployments, serves as a migration bridge for existing M2TS workflows, and presents a path toward MOQ as a first-class DVB IP transport layer. No implementation or vendor specifics are included.

---

## Audiences

- **DVB member organizations** (broadcasters, equipment vendors, network operators): need to understand where MOQ+M2TS fits in their existing infrastructure and why DVB should consider it as a recognized profile.
- **IETF MOQ Working Group participants**: need concrete DVB deployment scenarios to understand the real-world applicability of the MSFTS draft (`draft-gregoire-moq-msfts`).

Both audiences are served. The paper is self-contained — it does not assume familiarity with MSFTS or MOQT internals.

---

## Structural Approach

Option B — Standards Layering Document. Background and protocol stack content is presented systematically before deployment scenarios. The complement/bridge/replace analysis appears as a dedicated section after the scenarios, not as an upfront argument. Both audiences can navigate to the sections most relevant to them.

---

## Section Outline and Content Design

### Section 1 — Introduction (~400 words)

Frames the problem: DVB has standardized IP delivery via DVB-DASH (HTTP adaptive streaming over ISO BMFF) and DVB-NIP (GSE-encapsulated IP over satellite/terrestrial). Both assume HTTP/TCP at the application transport layer. As live latency requirements tighten and hybrid broadcast-broadband topologies grow more common, TCP head-of-line blocking and HTTP request-response semantics present limitations. QUIC-based transport — specifically MOQT — addresses these with multiplexed, partially-reliable, object-oriented delivery.

States the paper's purpose: to describe how MOQT carrying M2TS-packaged tracks via the MSFTS extension integrates with DVB infrastructure, and to articulate the standardization opportunity this represents for both DVB and IETF.

### Section 2 — Background (~800 words)

Five subsections, each self-contained:

**2.1 MPEG-2 Transport Stream and M2TS**
188-byte TS packets, 192-byte M2TS source packets with 4-byte arrival timestamp prefix, PAT/PMT/PCR/PTS/DTS, SCTE-35 splice signaling, single-program vs multi-program transport streams. Written for readers unfamiliar with the format.

**2.2 DVB-DASH**
MPEG DASH profile for DVB services over IP networks. ISO BMFF (fragmented MP4) container. HTTP-based ABR. Codec toolkit: AVC, HEVC, VVC, HE-AAC, AC-4. Service discovery via DVB-I. Validation tools provided by DVB.

**2.3 DVB Native IP Broadcasting (DVB-NIP)**
End-to-end native IP broadcast system. GSE encapsulation over DVB-S2X, DVB-S2, and DVB-T2 physical layers. DVB-MABR for multicast ABR delivery. Integration with DVB-I service discovery and DVB-DASH streaming. Hybrid broadcast+broadband architecture with satellite and terrestrial bearers.

**2.4 Media Over QUIC Transport (MOQT)**
QUIC as the transport protocol (RFC 9000). MOQT object model: namespace, track, group, object. Partial reliability: publishers and subscribers negotiate delivery priority; objects can be dropped without stalling the session. Relay architecture: MOQT relays cache and forward objects by MOQT metadata without parsing media payloads. Publisher and subscriber roles.

**2.5 MOQT Streaming Format (MSF) and MSFTS**
MSF defines a catalog model and common streaming conventions for tracks delivered over MOQT. MSFTS (`draft-gregoire-moq-msfts`) extends MSF by registering the `"m2ts"` packaging value. Key catalog fields: `m2tsPacketSize` (188 or 192), `m2tsProgramNumber`, `m2tsPmtPid`, `m2tsPcrPid`, `m2tsPsiInterval`, `m2tsRandomAccess`, `m2tsTimestampMode`, `m2tsScte35Pid`, `initData`. Object payload structure: concatenation of whole source packets, integer multiple of packet size. Group numbering tied to random access points (IDR or qualifying CRA frames).

### Section 3 — Protocol Stack (~500 words)

Presents the layered architecture as a stack comparison:

| Layer | DVB-DASH | DVB-NIP | MOQ+M2TS |
|---|---|---|---|
| Application | MPEG DASH | DVB-I / DVB-DASH | MOQT + MSFTS catalog |
| Media Packaging | ISO BMFF (fMP4) | ISO BMFF via MABR | M2TS / TS packets |
| Transport | HTTP/1.1 or HTTP/2 | HTTP/2 over MABR | QUIC / WebTransport |
| Encapsulation | TCP | GSE (DVB-NIP) | QUIC datagrams or streams |
| Physical | IP network | DVB-S2X, S2, T2 | DVB-S2X, S2, T2, or IP |

Central architectural claim: MOQ+M2TS replaces only the application and transport layers. The physical DVB bearers, GSE encapsulation, and existing M2TS content production pipelines are preserved.

Second sub-section: QUIC/WebTransport integration point. How MOQT sessions are established over QUIC (or WebTransport for browser endpoints). How MOQT relays fit into DVB headend and CDN topologies. How MOQT partial reliability maps to M2TS packet loss behavior: a missed object causes a stream discontinuity resolved at the next random access point, consistent with broadcast loss tolerance rather than TCP retransmission behavior.

### Section 4 — MSFTS Catalog Integration for DVB Services (~600 words)

Explains how DVB service tracks are described using MSFTS catalog fields, with JSON catalog examples in four DVB-relevant configurations:

**4.1 Single-program satellite feed**
`m2tsPacketSize: 192` (M2TS with arrival timestamp), `m2tsRandomAccess: true`, `m2tsPsiInterval` set to match DVB PSI repetition rates, `initData` carrying PAT+PMT encoded as Base64 for fast join at headend subscribers. `m2tsTimestampMode: "arrival-time"` for STC recovery precision.

**4.2 Multi-program terrestrial mux**
MPTS filtering: separate MOQT tracks per program, each carrying only its program's packets plus PAT (rewritten to list one program), PMT, PCR, and elementary stream PIDs. Null packet handling. `m2tsProgramNumber`, `m2tsPmtPid`, `m2tsPcrPid` fields. Independent programs published as separate tracks without `altGroup`.

**4.3 ABR alternate renditions**
`altGroup` field links tracks at different bitrates. Group boundaries must align at identical presentation positions across all tracks in the group. PCR discontinuity handling on track switch: receiver reinitializes STC from first PCR on the new track. PAT and PMT must be re-parsed after every track switch because PID assignments need not match across renditions.

**4.4 SCTE-35 and splice signaling**
`m2tsScte35Pid` advisory field. SCTE-35 splice_info_section() messages carried transparently in the TS stream on their designated PID. Relationship to DVB-DASH event stream signaling: MSFTS does not mandate SCTE-35 processing; publishers may optionally surface splice events via MSF Event Timeline.

### Section 5 — DVB Deployment Scenarios (~900 words)

Each scenario: topology → signal flow → MSFTS catalog configuration → key operational considerations.

**5.1 Satellite Contribution and Distribution (DVB-S2/S2X)**
Live event or studio-to-headend contribution feed encoded as M2TS (192-byte source packets). MOQT publisher at the uplink facility. MOQT relay at or near the satellite uplink. Downstream headends subscribe over GSE-encapsulated IP on DVB-S2X. PCR continuity preserved across MOQT group boundaries (discontinuity_indicator bit set only between groups where a PCR discontinuity is intentionally introduced). 192-byte M2TS preferred for contribution: arrival timestamp supports precise STC recovery at receiving headends. `initData` carrying PAT+PMT enables fast group join without waiting for PSI repetition cycle.

**5.2 Terrestrial Multicast Distribution (DVB-T2)**
Multi-program transport stream from a regional headend distributed to DVB-T2 transmitter network via MOQT. MPTS filtered at MOQT publisher into per-program tracks. DVB-T2 transmitters subscribe to required programs and reconstruct a local MPTS for over-the-air emission. `m2tsPsiInterval` bounds maximum join latency at transmitter sites. PAT rewriting rules per MSFTS spec ensure each track presents as a valid SPTS. Null packet handling: publishers may retain or remove null packets at their discretion.

**5.3 Hybrid Broadcast-Broadband (DVB-NIP + QUIC Unicast)**
DVB-NIP satellite multicast feed (DVB-MABR) augmented with MOQT unicast delivery for broadband-only devices or for ABR adaptation beyond MABR capability. MOQT relay bridges the two paths: ingests from the broadcast feed, republishes as MOQT tracks over QUIC. Subscribers in broadband-only coverage receive the same M2TS-packaged content. `altGroup` links satellite and unicast renditions where they carry the same content at different bitrates. Group boundary alignment and PTS alignment across renditions enable seamless presentation switching at the application layer.

### Section 6 — Relationship to Existing DVB Standards (~600 words)

**6.1 Complement**
MOQ+M2TS requires no changes to DVB physical layers, GSE, DVB-I service discovery, codec profiles, or content protection. Transport-stream scrambling and conditional access are opaque to MOQT relays. Operators can deploy MOQT alongside DVB-DASH for low-latency or contribution use cases without displacing existing infrastructure.

**6.2 Bridge**
Existing M2TS production workflows — encoders, muxers, playout systems — require no re-encoding or re-packaging. MSFTS maps the existing packet stream directly into MOQT objects. This is the key migration advantage over DVB-DASH, which requires ISO BMFF re-wrapping of elementary streams. The `initData` field and PSI repetition rules allow existing DVB service information to be carried without modification.

**6.3 Replacement Path**
For greenfield IP-only deployments or next-generation DVB profiles, MOQ+M2TS provides a unified transport layer for contribution and distribution, replacing the HTTP/TCP stack of DVB-DASH with QUIC while retaining M2TS as the media container. MOQT partial reliability maps to broadcast loss tolerance more naturally than TCP retransmission. MOQT relay caching provides CDN-like distribution without requiring HTTP infrastructure.

### Section 7 — Standardization Path (~400 words)

**7.1 IETF MOQ Working Group**
`draft-gregoire-moq-msfts` is an informational extension to `draft-ietf-moq-msf`. The DVB deployment scenarios in this paper constitute concrete evidence of real-world applicability supporting the draft's progression. Two areas where DVB use cases may inform future MSFTS revisions: PSI repetition rate signaling in live contribution feeds; relay behavior for hybrid broadcast-broadband topologies.

**7.2 DVB**
MOQ+M2TS is a candidate profile for a future DVB specification analogous to DVB-DASH: a constrained profile of MOQT+MSF+MSFTS tailored to DVB service delivery requirements. Proposed scope for a DVB study mission or technical module: codec and bitrate constraints for DVB service types, PSI repetition requirements for live contribution and distribution, DVB-I service discovery integration for MOQT-delivered services, interoperability requirements with DVB-NIP multicast infrastructure. The paper calls on DVB members to evaluate MOQ+M2TS in their deployment contexts and contribute findings to both DVB and IETF.

### Section 8 — Conclusion (~200 words)

Restates the three-part argument: MOQ+M2TS complements existing DVB-DASH and DVB-NIP deployments without disrupting infrastructure; bridges existing M2TS production workflows into QUIC-based delivery without re-encoding; and provides a credible replacement path for HTTP-based transport in future DVB IP profiles. Closes by framing MSFTS as the technical foundation enabling this trajectory, and inviting engagement from DVB members and IETF MOQ Working Group participants.

### Section 9 — References

**Normative:**
- ISO/IEC 13818-1 — MPEG-2 Systems (Transport Stream)
- draft-ietf-moq-transport — Media Over QUIC Transport
- draft-ietf-moq-msf — MOQT Streaming Format
- draft-gregoire-moq-msfts — MPEG-2 TS Packaging for MOQT
- ETSI EN 303 560 — DVB Native IP Broadcasting (DVB-NIP)
- ETSI EN 303 285 — DVB MPEG-DASH Profile (DVB-DASH)
- DVB-S2: ETSI EN 302 307
- DVB-S2X: ETSI EN 302 307-2
- DVB-T2: ETSI EN 302 755
- RFC 9000 — QUIC: A UDP-Based Multiplexed and Secure Transport

**Informative:**
- DVB-I: ETSI TS 103 770
- DVB-MABR: ETSI TS 103 769
- SCTE-35 — Digital Program Insertion Cueing Message
- draft-ietf-moq-secure-objects
- draft-ietf-moq-c4m
- draft-ietf-moq-privacy-pass-auth

---

## Constraints

- No implementation or vendor specifics
- No reference implementation section
- Self-contained: sufficient MSFTS and MOQT explanation for readers unfamiliar with the drafts
- Covers both DVB-S2/S2X (satellite) and DVB-T2 (terrestrial) bearers
- Hybrid broadcast+broadband scenarios included
- Dual standardization call-to-action: DVB and IETF MOQ WG

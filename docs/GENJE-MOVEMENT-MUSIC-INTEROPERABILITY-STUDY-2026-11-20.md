# GENJE — Movement and Music Interoperability Study

**Date:** 2026-11-20  
**Status:** RESEARCH / COMPARATIVE TECHNICAL STUDY  
**Owner:** GENJE — movement, choreography, sound, performance and embodied creative practice  
**Related domains:** WARENA — infrastructure and reproducibility; IKAI — participant-directed reflection; FELOH Corpus — shared evidence, provenance and governance  
**Implementation status:** Desk study and proposed test plan only. No import/export adapter, parser, converter, runtime integration or empirical round-trip test is claimed as implemented.

## 1. Executive decision

Do not create a new replacement for established movement notation, motion-capture formats, 3D interchange formats or music/event protocols.

The formats solve different problems:

- **Labanotation / Kinetography Laban** is a symbolic movement notation authored and interpreted by trained people.
- **Motif** is a selective movement-description approach, not a full transcription.
- **BVH** represents a skeleton hierarchy and sampled joint animation.
- **C3D** stores measured 3D points and analogue channels with measurement parameters and sampling information.
- **FBX** exchanges complex 3D scenes and animation within a vendor-controlled ecosystem.
- **OSC** transports structured messages and time-tagged bundles for interactive systems.
- **MIDI** transports musical/device events; Standard MIDI Files store timestamped event sequences in musical or SMPTE time.
- **TidalCycles** provides cycle-based musical pattern timing and can emit OSC or MIDI.

These are complementary layers, not rival universal standards.

**Recommended integration posture:**
1. Keep the existing GENJE Movement IR proposal as the semantic integration contract, not a replacement file format.
2. Keep human-authored scores and notation as first-class source artefacts.
3. Use C3D for measured capture data where available; BVH for simple skeleton-animation interchange; FBX only where an external production pipeline requires it.
4. Use OSC for live event transport and MIDI/SMF for musical/device interoperability.
5. Preserve source files, coordinate conventions, clock domains, units, provenance and transformation reports.
6. Require human review for every semantic translation between measured motion and symbolic notation.

## 2. Research question and method

**Question:** Which existing formats can exchange movement, music and performance timing without silently destroying important information, and what minimal integration metadata is needed to make their boundaries explicit?

This is a documentary comparison of official format documentation, established notation references and the existing GENJE research documents. It is not an empirical compatibility benchmark.

Evidence classes:
- **FORMAT DOCUMENTED:** directly supported by a format or tool's documentation.
- **DESIGN INFERENCE:** a consequence of the documented format scope.
- **PROPOSED TEST:** an experiment not yet run.
- **NOT TESTED:** no executable parser, converter or live system has been exercised in this study.

## 3. Capability comparison

| Artefact / protocol | Native representation | Timing model | Spatial/body model | Context / semantics | Primary use |
|---|---|---|---|---|---|
| Labanotation / Kinetography Laban | Symbols arranged on a movement staff | Symbol duration and vertical score progression | Body-part columns, direction and level | Human-readable movement instructions; interpretation depends on notation knowledge | Authored movement score |
| Motif Description | Selected actions, stillness and salient movement ideas | Selective score timing | Broad movement concepts | Intentionally abstract | Composition, teaching and analysis |
| BVH | Hierarchy, offsets, channels and sampled motion values | Fixed frame interval per motion sequence | Joint hierarchy and channels | Sparse; no rich choreographic or cultural ontology | Skeleton animation interchange |
| C3D | 3D point samples, residual/quality values, analogue channels and parameters | Point rate; analogue samples at integer multiples per point frame | Calibrated measurement-space coordinates and labelled points | Measurement and lab metadata through parameters | Motion-capture and biomechanics interchange |
| FBX | Scene graph, transforms, meshes, cameras, lights and animation | Animation curves and scene time settings | Rich scene and rig representation | Application/SDK-specific scene metadata | 3D production exchange |
| OSC | Addressed, typed messages and bundles | Optional absolute NTP-style time tags in bundles | No native body model | Application-defined message semantics | Real-time event transport |
| MIDI 1.0 / SMF | Channel/system messages; SMF tracks and meta-events | Delta ticks with PPQN+tempo map or SMPTE time division | No native body model | Musical events, track names, tempo, meter and markers | Musical device and sequence exchange |
| MIDI 2.0 / UMP | Extended MIDI messages in Universal MIDI Packets | Optional transport jitter-reduction timestamps; clip timing mechanisms | No native body model | Richer per-note control and capability negotiation | Higher-resolution musical/device exchange |
| TidalCycles | Patterns evaluated in cycles | Cycles per second, with tempo/cycle relationships | No native body model | Pattern transformations and musical structure | Live-coded music and OSC/MIDI output |

References:
- Ohio State University, Labanotation, Motif and LMA overview: https://dance.osu.edu/research/dnb/resources
- C3D specification: https://www.c3d.org/HTML/Documents/specification.htm
- C3D file structure: https://www.c3d.org/HTML/Documents/thec3dfilestructure.htm
- Blender BVH importer/exporter: https://docs.blender.org/manual/en/latest/files/import_export/bvh.html
- Autodesk FBX technology: https://help.autodesk.com/cloudhelp/2020/ENU/FBX-Developer-Help/files/welcome_to_the_fbx_sdk/FBX_Developer_Help_welcome_to_the_fbx_sdk_what_is_autodesk_fbx_technology_html.html
- OSC 1.1 and temporal semantics: https://opensoundcontrol.stanford.edu/spec-1_1.html
- MIDI 2.0: https://midi.org/midi-2-0
- MIDI UMP and MIDI 2.0 protocol: https://midi.org/universal-midi-packet-ump-and-midi-2-0-protocol-specification
- TidalCycles time: https://tidalcycles.org/docs/getting-started/tutorial/
- TidalCycles OSC: https://tidalcycles.org/docs/configuration/MIDIOSC/osc/

## 4. Format-by-format assessment

### 4.1 Labanotation and Motif

Labanotation is a symbolic notation system. The Ohio State University Department of Dance summarises its symbol components as direction, level, timing and the body part involved, arranged on a staff read from bottom to top and left to right. Motif Description intentionally reduces the record to essential actions and stillness.

**Reuse decision:** do not encode a GENJE-specific replacement for these systems. Preserve the notation score, notation method, version/lineage, author/notator, teaching or review context, and a link to any associated performance record.

**Adapter boundary:** a notation adapter may associate score passages and movement events with a GENJE work/session identifier and timeline. It must not silently translate every notation symbol into a guessed joint angle or a sensor label. A human notator's interpretation is not equivalent to measured kinematics.

**Information at risk in digitisation:**
- symbol geometry and layout;
- staff reading order;
- body-part placement;
- duration and simultaneity;
- notation-specific conventions and variants;
- editorial marks, corrections and uncertainty;
- context supplied in the score's accompanying documentation.

A score-image OCR process, if ever evaluated, would produce candidate transcription requiring trained human review.

### 4.2 BVH

Blender's current manual documents BVH import/export for skeleton hierarchy and animation. Its importer exposes scale, rotation order, forward/up axis mapping, frame-rate scaling and scene timing controls. Blender uses Y-forward and Z-up by default, while other systems may use different conventions.

**Reuse decision:** BVH is a useful simple skeleton-motion interchange format and a reasonable first animation adapter.

**Do not assume:** two BVH files with the same joint labels have identical skeleton semantics, rest poses, units, coordinate axes or rotation conventions.

**Required sidecar metadata for reliable exchange:**
- skeleton identifier and hierarchy version;
- joint names and parent relationships;
- rest-pose/reference-pose description;
- axis convention and handedness;
- units and scale;
- rotation order and channel ordering;
- frame rate and frame count;
- root translation policy;
- source capture method and any retargeting;
- missing joints, interpolation and filtering operations.

BVH does not carry GENJE's authorship, movement interpretation, cultural context, group relationships or musical intent. Preserve those in the GENJE record and link the file.

### 4.3 C3D

C3D is designed to store 3D point locations together with analogue measurements in one documented structure. Its header, parameter and data sections describe the recorded data. It can store point residuals/quality information, sample rates, labels and analogue channels. Multiple analogue samples can be associated with each 3D point frame.

**Reuse decision:** prefer C3D as a research interchange artefact when the source is a motion-capture or biomechanics system producing measured point and analogue data.

**Important limitation:** C3D's data synchronisation describes how samples are stored together; it does not guarantee that every sensor was physically synchronised correctly at acquisition. The C3D documentation explicitly notes that the collection system determines temporal synchronisation and that filtering can introduce channel-specific latency.

**Required metadata:**
- point and analogue rates;
- point labels and units;
- coordinate origin and axes;
- residuals/quality and camera contribution where present;
- analog channel units, scaling and filtering;
- acquisition system and calibration record;
- known latency and clock offset;
- missing/occluded samples and reconstruction operations.

C3D is a measurement container, not a dance score. Converting C3D points into a skeleton requires marker assignment, body model assumptions and often inverse kinematics. Those steps are an interpretation pipeline and must be reported.

### 4.4 FBX

Autodesk describes FBX as a 3D scene interchange technology that can store cameras, lights, meshes, NURBS and other scene elements. Autodesk's developer documentation states that the FBX file format is not documented and recommends using the FBX SDK for reading/writing. The SDK is governed by Autodesk's own terms and is not GPL.

**Reuse decision:** support FBX only as an optional production boundary when a collaborator, studio or animation pipeline needs it. Do not make it the canonical archive or a required dependency of the WARENA stack.

**Risks:**
- vendor-controlled SDK and licensing;
- version differences;
- hidden application-specific data;
- scene conversion losses;
- more data than a movement interchange task needs;
- proprietary SDK dependencies that complicate libre-first reproducibility.

Where practical, retain a C3D or BVH source plus a documented export package rather than only an FBX deliverable.

### 4.5 OSC

OSC messages use address patterns, type tags and typed arguments. OSC bundles group messages under a time tag. The OSC 1.0 specification describes a 64-bit NTP-style timestamp and immediate execution semantics for single messages. OSC does not provide its own clock-synchronisation mechanism.

**Reuse decision:** OSC is the preferred live event bridge between movement score cues, TidalCycles, SuperCollider, visual systems and other real-time tools where endpoints support it.

**Do not treat OSC as:**
- a persistent score archive;
- a source of clock truth;
- a complete event schema;
- a delivery guarantee over an unreliable network.

A GENJE OSC profile would need explicit address names, argument types, units, versioning, event identifiers, clock interpretation and error handling. Keep the profile small and application-specific. It is not a new transport protocol.

### 4.6 MIDI 1.0, Standard MIDI Files and MIDI 2.0

MIDI 2.0 extends rather than replaces MIDI 1.0, retaining compatibility as a design priority. It adds higher-resolution channel voice data and richer per-note control. UMP provides a common packet structure; MIDI 2.0 also defines capability negotiation and property exchange.

Standard MIDI Files store events with delta-time ticks. In metrical time, ticks are interpreted through ticks-per-quarter-note and tempo events; alternatively the time division can use SMPTE. The meaning of a beat also depends on meter and musical context.

**Reuse decision:** use MIDI for musical events, device control and compatible performance cues. Use SMF for an exchangeable musical event sequence where that is the actual artefact.

**Do not use MIDI as a movement ontology.** A note-on event can trigger a movement cue or a lighting change, but it does not describe the movement itself.

**MIDI 2.0 decision:** retain as a forward-looking compatibility option. Do not require MIDI 2.0 hardware or implement a MIDI 2.0-only system in the first interoperability experiment.

### 4.7 TidalCycles timing

Tidal's core timing unit is cycles per second (CPS). Its documentation explains how to relate BPM to CPS by deciding how many beats are contained in a cycle. Tidal can send patterned OSC messages and can control other systems through OSC or MIDI.

**Integration implication:** GENJE must preserve the mapping between cycles, beats, meter, tempo and performance time. A cycle is not inherently a bar: that relationship is a chosen pattern/tempo convention. Tempo changes, polyrhythms, swing and pattern transformations must not be flattened into a single BPM number.

## 5. Time and synchronisation: the highest-risk interoperability boundary

Movement and music systems often use different clocks:

| Clock domain | Typical representation | Common failure |
|---|---|---|
| Score time | Ordered symbols, durations and phrase boundaries | Assumed exactness where notation is intentionally qualitative |
| Musical time | Bar, beat, subdivision, tempo and meter | Treating all beats as quarter notes or assuming constant tempo |
| MIDI SMF time | Delta ticks plus PPQN/tempo map or SMPTE | Converting ticks to seconds using only the initial tempo |
| Tidal time | Cycles and CPS | Assuming one cycle equals one bar |
| BVH time | Fixed frame interval | Frame-rate resampling and dropped/duplicated frames |
| C3D time | Point rate and analogue samples per point frame | Acquisition latency or filtered channel delay |
| OSC time | Bundle timetags using an absolute time representation | Assuming clocks on separate hosts are synchronised |
| Audio time | Sample index and sample rate | Device buffer latency and clock drift |
| Video time | Frame index, frame rate and presentation timestamps | Variable frame rate and dropped frames |
| Wall-clock time | Host clock / monotonic clock | Wall-clock adjustment and host-to-host offset |

### 5.1 Proposed time contract

The GENJE integration layer should retain both:

1. **Musical position:** a structured relation to a named musical timeline, including meter, tempo map, beat/subdivision or cycle position.
2. **Performance-clock position:** a measured or scheduled time relative to a named clock origin, with clock identity and uncertainty.

Do not store only a floating-point timestamp and assume it is universal.

For each linked stream, record:
- clock domain identifier;
- clock origin and reference;
- units and resolution;
- rate or tempo map;
- offset relative to the session timeline;
- estimated drift where known;
- measured or assumed latency;
- uncertainty and method of estimation;
- whether the value is authored, scheduled, observed or measured.

Where exact arithmetic matters, use rational or integer time units at the boundary and convert to device-specific formats only at export. Preserve the original values and conversion rule.

### 5.2 Synchronisation policy

- OSC timetags schedule messages but do not synchronise independent clocks.
- C3D sample interleaving preserves recorded sample relationships but cannot correct bad acquisition synchronisation.
- MIDI tick values require the correct tempo map or SMPTE division.
- Tidal CPS must be related to beats-per-cycle and meter explicitly.
- Audio and video require their own sample/frame clocks.
- Any inferred alignment must carry an uncertainty estimate and be labelled inferred.

## 6. Transformation and information-loss matrix

| Source → target | What can map | What is lost or needs a sidecar | Human review |
|---|---|---|---|
| Labanotation → Movement IR | Score passages, body-part references, direction/level and timing where parsed | Symbolic notation details, notator's reading, convention and visual layout | Required for semantic transcription |
| Motif → Movement IR | Abstract actions, stillness and phrase annotations | Intentionally omitted detail cannot be reconstructed | Required for interpretation |
| Movement IR → BVH | Selected joint transforms and sampled animation | Cultural semantics, authorship, qualitative effort, group relations, notation symbols | Required before publication/use |
| BVH → Movement IR | Skeleton hierarchy, sampled transforms and frame times | Choreographic meaning, intent, contact semantics and score interpretation | Required for any semantic labels |
| C3D → BVH | Estimated skeleton motion from marker trajectories | Raw markers, residuals, analogue channels, acquisition details unless separately retained | Required for marker assignment and IK |
| BVH → C3D | Possible point trajectories derived from a rig | Original measured points and sensor residuals cannot be recreated | Required; output must be labelled synthetic/derived |
| C3D → Movement IR | Linked measured tracks and sample metadata | Symbolic score and cultural interpretation | Required for interpretation |
| Movement IR → OSC | Live cues, IDs, selected values and scheduled times | Persistent context, long-form score, full provenance unless separately referenced | Required for cue design |
| OSC → Movement IR | Received event logs and timestamps | Missing messages, sender clock uncertainty, unrecorded context | Required before treating as a score |
| MIDI/SMF → Movement IR | Tempo, meter, musical markers and selected cue events | Movement semantics and performance interpretation | Required for movement mapping |
| Movement IR → MIDI/OSC | Selected cue events and musical control | Fine-grained score structure and context | Required to author mapping |
| FBX ↔ BVH/C3D | Some skeleton/animation or scene data | Scene features, rig metadata, units, constraints and proprietary extensions | Required for production conversion |

**Non-negotiable rule:** every transformation must produce a loss report. A successful file export is not proof of semantic preservation.

## 7. Proposed adapter contract

This is a boundary contract, not a new file format or final schema.

Each adapter should expose:

1. **Identity:** adapter name, version, source format, target format and implementation version.
2. **Input identity:** source file hash, source record ID and rights/access classification.
3. **Assumptions:** skeleton map, coordinate axes, units, frame rate, tempo map and clock origin.
4. **Transformations:** resampling, interpolation, filtering, retargeting, quantisation, marker assignment and inferred values.
5. **Output identity:** output file hash, output format version and associated GENJE work/session IDs.
6. **Loss report:** fields preserved, transformed, omitted, approximated, inferred or unsupported.
7. **Uncertainty:** measurement quality, timing uncertainty and semantic confidence where meaningful.
8. **Human review:** reviewer identity/role, decision, corrections and date—only where authorised and appropriate.
9. **Rights:** source licence, performer consent, allowed use, expiry and redistribution restrictions.

Adapter outcomes should be explicit:
- preserved
- transformed
- approximated
- inferred
- omitted
- unsupported
- requires-human-review

These are transformation statuses, not quality ratings of a performer or tradition.

## 8. Recommended minimal interoperability profile

### 8.1 First experiment

Choose a short, practitioner-authored movement phrase and an accompanying musical phrase. Obtain explicit permission for the exact research operations. The phrase should be authored by the participating practitioner; this study does not invent or prescribe its choreography.

Create a linked package containing:
- original human-authored score or notation;
- practitioner explanation and allowed context;
- audio or musical event sequence where rights permit;
- optional video reference with explicit consent;
- a simple BVH animation only if a suitable skeleton representation is available;
- C3D only if a genuine measured capture source is available;
- source and transformation metadata;
- practitioner corrections and review record.

Do not begin by collecting a large dataset. One fully documented phrase can expose more interoperability problems than a large unreviewed capture set.

### 8.2 Round-trip tests

| Test | Operation | Expected evidence |
|---|---|---|
| T01 — Notation preservation | Archive score and metadata; render/view without semantic conversion | Original score remains readable, attributed and versioned |
| T02 — BVH import/export | Import sample BVH into Blender, export, re-import | Joint hierarchy, frame count, axes, scale and frame timing differences recorded |
| T03 — C3D inspection | Read official sample C3D; inspect point/analogue rates and parameters | Units, labels, residuals, sampling and synchronisation metadata preserved |
| T04 — C3D-to-skeleton | Derive a skeleton only where markers and model are documented | Marker assignment, IK assumptions and residual errors reported |
| T05 — Musical timing | Read SMF with tempo/meter changes | Event positions and tempo-map conversions verified |
| T06 — Tidal/OSC bridge | Emit a small authored cue pattern and receive scheduled OSC bundles | Event IDs, clock mapping, latency and jitter measured |
| T07 — Cross-clock alignment | Compare audio, OSC, MIDI and movement event markers | Offset, drift and uncertainty reported |
| T08 — Practitioner review | Compare original phrase, score, render and event mapping | Corrections, disagreements and usefulness documented by practitioner |
| T09 — Loss-report validation | Deliberately remove/alter a field during conversion | Adapter identifies loss and does not claim exact equivalence |
| T10 — Rights/withdrawal test | Remove an authorised test contribution from the research package | Copies, derived files and access records are traceable and deletable as agreed |

### 8.3 Pass criteria

A test passes only when:
- the source artefact remains available and unchanged;
- coordinate and time conventions are explicit;
- conversion errors are measurable or marked unknown;
- no unsupported semantic claim is introduced;
- rights and consent remain attached to the derivative;
- a human can identify what changed;
- round-trip loss is documented, not hidden.

There is no universal numeric tolerance for all movement tasks. Tolerances must be selected for the task and capture method, with practitioner and technical input.

## 9. ATUNDA and African-centred evaluation

ATUNDA is an important comparative research neighbour, not a dataset GENJE can freely absorb. Its repository describes 964 video sequences and 49 movement categories, with a custom non-commercial licence and deletion conditions. The project is a source for methodological comparison and possible scholarly contact.

For the interoperability experiment:
- study the published data structure and movement taxonomy;
- do not copy restricted media or annotations into GENJE;
- distinguish ATUNDA's labels from a community's own movement terminology;
- do not equate classifier similarity with cultural equivalence or ownership;
- ask researchers and relevant practitioners about their representation and governance choices;
- use GENJE-authored and rights-cleared material for any independent experiment.

Source: https://github.com/digitalworlds/atunda  
Associated IMX 2026 paper: https://doi.org/10.1145/3788851.3805020

The evaluation should be co-designed with the relevant practitioner(s). Their review must be able to reject a mapping, preserve alternate interpretations and identify aspects that should not be recorded or published.

## 10. Tool and infrastructure decisions

| Candidate | Decision | Reason |
|---|---|---|
| Blender | First visual inspection target | Existing BVH import/export and mature 3D inspection; no need to build a viewer |
| C3D tools/readers | Use existing reader for sample inspection | C3D has documented structure and test files |
| Guile/Scheme | Preferred orchestration and metadata layer in WARENA | Fits existing local-first/reproducible architecture |
| SQLite | Local index and metadata store | Mature local persistence; do not embed large raw media unnecessarily |
| OSC | Preferred real-time message bridge | Existing protocol and Tidal/SuperCollider ecosystem support |
| MIDI/SMF | Musical event interchange | Established musical semantics and compatibility |
| TidalCycles | Livecoding timing and event source | Existing cycle-based pattern engine |
| SuperCollider | Sound generation and timing endpoint | Existing GENJE livecoding research candidate |
| FBX SDK | Optional external boundary only | Autodesk-controlled SDK and format ecosystem |
| Python-based conversion utilities | Isolated compatibility tools where needed | Useful upstream ecosystem; not the canonical WARENA runtime |
| New custom motion format | Do not create | Existing formats cover measurement, animation, notation and transport layers |

## 11. Technical risks

1. **Coordinate errors:** axis, handedness, unit, root transform and rotation-order mismatches can make a correct file appear wrong.
2. **Skeleton mismatch:** joint names do not guarantee equivalent anatomical or rig semantics.
3. **Resampling:** conversion between frame rates can alter event timing and extrema.
4. **Filtering latency:** sensor processing can shift signals relative to other channels.
5. **Tempo-map loss:** constant-tempo conversion can misplace events after tempo changes.
6. **Cycle ambiguity:** a Tidal cycle is not necessarily a bar or phrase.
7. **Network timing:** OSC bundles do not establish clock synchronisation.
8. **Semantic overreach:** mapping measured velocity to LMA Effort or cultural style without validation creates false claims.
9. **Rights leakage:** derivative files remain subject to relevant source and participant restrictions.
10. **Vendor dependency:** FBX SDK terms and proprietary extensions complicate libre-first workflows.

## 12. Recommended sequence

**I0 — Documentation complete:** format and clock comparison, adapter contract, loss matrix and test plan.  
**I1 — Sample-file inspection:** select lawful sample BVH, C3D and SMF fixtures; record provenance and checksums.  
**I2 — Manual baseline:** select a practitioner-authored score and establish the human reference record.  
**I3 — Blender BVH round trip:** inspect and quantify import/export differences.  
**I4 — C3D data audit:** inspect point/analogue values, metadata and timing.  
**I5 — MIDI/Tidal timing:** verify tempo maps, cycles and event positions.  
**I6 — OSC live bridge:** test scheduling, latency, clock offset and event delivery.  
**I7 — Human evaluation:** practitioner review of score, visualisation and mapped cues.  
**I8 — Implementation decision:** implement only adapters shown to provide real value and acceptable loss.

No I1–I8 work is claimed complete by this document.

## 13. Source register

### Format specifications and official tool documentation
- C3D specification: https://www.c3d.org/HTML/Documents/specification.htm
- C3D file structure: https://www.c3d.org/HTML/Documents/thec3dfilestructure.htm
- C3D synchronisation: https://www.c3d.org/HTML/Documents/datasynchronization.htm
- C3D point units: https://www.c3d.org/HTML/Documents/3dpointdata.htm
- Blender BVH manual: https://docs.blender.org/manual/en/latest/files/import_export/bvh.html
- Autodesk FBX technology: https://help.autodesk.com/cloudhelp/2020/ENU/FBX-Developer-Help/files/welcome_to_the_fbx_sdk/FBX_Developer_Help_welcome_to_the_fbx_sdk_what_is_autodesk_fbx_technology_html.html
- Autodesk FBX SDK: https://aps.autodesk.com/developer/overview/fbx-sdk
- OSC 1.1 contents/specification: https://opensoundcontrol.stanford.edu/toc.html
- OSC 1.0 temporal semantics: https://opensoundcontrol.stanford.edu/spec-1_0.html
- MIDI 2.0: https://midi.org/midi-2-0
- MIDI UMP and MIDI 2.0 protocol: https://midi.org/universal-midi-packet-ump-and-midi-2-0-protocol-specification
- Standard MIDI Files: https://midimusic.github.io/tech/midispec.html
- TidalCycles tutorial/time: https://tidalcycles.org/docs/getting-started/tutorial/
- TidalCycles OSC: https://tidalcycles.org/docs/configuration/MIDIOSC/osc/

### Notation and movement research
- Ohio State University Department of Dance resources: https://dance.osu.edu/research/dnb/resources
- International Council of Kinetography Laban: https://ickl.org/
- Dance Notation Bureau: https://dancenotation.org/

### African-centred computational dance research
- ATUNDA repository: https://github.com/digitalworlds/atunda
- ATUNDA IMX 2026 paper: https://doi.org/10.1145/3788851.3805020

## 14. Relationship to canonical GENJE research

This study supplements, and does not replace:
- [GENJE Movement IR and Motion Research](GENJE-MOVEMENT-IR-AND-MOTION-RESEARCH-2026-11-20.md) — semantic integration proposal.
- [GENJE Technology, Scholarly & Industry Landscape](GENJE-TECHNOLOGY-SCHOLARSHIP-INDUSTRY-LANDSCAPE-2026-11-20.md) — broad scholarly, technology, industry and governance landscape.
- [Labanotation, Movement Scores and Choreohacking](LABANOTATION-MOVEMENT-SCORE-RESEARCH-2026-11.md) — human-authored notation and plural documentation.
- [Kinetics, Livecoding & IKAI Interaction](KINETICS-LIVECODING-AND-IKAI-INTERACTION-2026-11-18.md) — creative system and time-stream research.
- [Embodied Spatial Interaction Research](EMBODIED-SPATIAL-INTERACTION-RESEARCH-2026-11-14.md) — optional spatial/XR context.

**Final position:** GENJE should own the creative and contextual relationships between these established systems, not recreate their underlying technologies. Preserve original artefacts, make conversions inspectable, and treat practitioner review and rights provenance as part of technical correctness.

# GENJE — Movement Notation and Interoperability Validation

**Date:** 2026-11-24  
**Status:** RESEARCH / PROPOSED VALIDATION PROTOCOL  
**Relationship:** Supplements the existing Movement IR, Labanotation and Movement/Music Interoperability studies.  
**Implementation:** No parser, converter, notation corpus, motion-capture pipeline or round-trip benchmark is claimed as implemented.

## 1. Do not collapse distinct movement records

GENJE's existing Movement IR direction is sound: keep these artefacts separate and link them through explicit, reviewable adapters.

1. Human-authored choreography / score.
2. A notation transcription made by a trained notator.
3. An observed performance and its context.
4. A sensor measurement with calibration and uncertainty.
5. A digital skeleton/animation representation.
6. A musical or event timeline.
7. A researcher's interpretation.

A conversion may preserve some information while losing other information. The source artefact must remain intact, and every transformation must identify its software/version, settings, coordinate system, timebase, author and known loss.

## 2. Established notation and archival practice

### Labanotation / Kinetography Laban

Labanotation is a symbolic movement-notation system with a trained reading and writing practice. The Library of Congress Dance Notation Collection finding aid identifies historical Labanotation and Benesh scores as distinct archival holdings. Harvard Library's performing-arts research guide likewise treats dance notation as a family of systems rather than one universal notation.

- [Library of Congress — Dance Notation Collection](https://tile.loc.gov/storage-services/service/gdc/gdcfindingaidpdfs/mu020028/mu020028.pdf)
- [Harvard Library — Primary Sources for Performing Arts Research: Dance Notation](https://guides.library.harvard.edu/c.php?g=1294023&p=9509243)
- [Ohio State University Department of Dance — Research and notation resources](https://dance.osu.edu/research/dnb/resources)

### Benesh Movement Notation

Benesh Movement Notation is a separate system with its own history, notation practice and institutional lineage. Do not translate between Benesh and Labanotation by mapping symbols one-to-one.

- Victoria J. Watts, “Benesh Movement Notation and Labanotation: From Inception to Establishment (1919–1977),” *Dance Chronicle* 38(3), 2015, pp. 275–304. [DOI: 10.1080/01472526.2015.1085227](https://doi.org/10.1080/01472526.2015.1085227).

### Motif

Motif is a selective movement-description approach, not a full kinematic transcription. Keep its abstraction level visible and do not expand a motif into exact joint trajectories without independent evidence.

**Governance:** notation is not a neutral substitute for embodied knowledge. Record the notator, performer/choreographer, teaching lineage or interpretive context where supplied, and any limits on access or reuse. A public score or archive catalogue does not grant permission to republish a protected work or culturally restricted knowledge.

## 3. Interoperability boundary

Retain the existing format roles:

| Format / protocol | Suitable role | Required metadata / caveat |
|---|---|---|
| Labanotation | Human-authored symbolic score | Notation version, author/notator, staff layout, reading order, corrections and rights |
| Benesh | Human-authored symbolic score | Benesh-specific conventions and provenance; no assumed symbol equivalence with Labanotation |
| Motif | Selective conceptual score | Explicit abstraction and omissions |
| C3D | Measured 3D points and analogue channels | Calibration, units, sampling rates, labels, residuals and laboratory context |
| BVH | Skeleton hierarchy and sampled animation | Axis, handedness, units, rest pose, hierarchy, channel order and frame rate |
| FBX | Scene/rig/animation exchange where required | Application/SDK version, export options and proprietary-tool dependency |
| OSC | Live structured event transport | Address schema, type tags, bundle time tags and clock mapping |
| MIDI / SMF | Musical/device event and sequence exchange | PPQN/tempo map or SMPTE division, track/event order and timing semantics |

The GENJE Movement IR remains a semantic integration layer, not a replacement for any of these formats. Preserve original files and produce a transformation report for every import/export.

## 4. Proposed round-trip and conformance tests

Use a small, deliberately authored, rights-cleared test suite before any participant movement capture.

**Fixture A — score structure**
- One authored phrase with stillness, transition, direction change and simultaneous body-part actions.
- Record the source score and the author's intended reading.
- Check whether digitisation preserves symbol geometry, ordering, simultaneity and editorial marks.

**Fixture B — timing**
- Create events with known beat positions, durations and deliberate offsets.
- Convert to the selected event representation and back.
- Report absolute timing error, accumulated drift, dropped/duplicated events and rounding behaviour.

**Fixture C — spatial coordinates**
- Use synthetic points and a declared coordinate frame.
- Test axis conversion, handedness, units, origin, scale and rotation order.
- Report maximum and RMS positional error.

**Fixture D — missing/uncertain data**
- Introduce missing points, low-confidence/residual values and clock gaps.
- Confirm the adapter preserves missingness and uncertainty rather than silently interpolating or inventing a movement.

**Fixture E — human interpretation**
- Ask the original author/notator or an appropriately qualified reviewer to inspect the converted score.
- Record disagreement and interpretive ambiguity; do not treat a numeric similarity score as proof of semantic equivalence.

For each test, preserve source file, output file, converter revision, settings, raw diff, test script, expected result and actual result. An adapter is not validated merely because it can open and save a file.

## 5. Performance and synchronization metrics

For live audiovisual work, record:
- event-to-audio onset error;
- audio/video/movement clock offset and drift;
- OSC bundle scheduling error;
- MIDI event timing error and jitter;
- missing, duplicated and reordered events;
- buffer depth, underruns and recovery after interruption.

Report p50/p95/p99, maximum, sample count, clock source and measurement uncertainty. Do not compare latency values from different clock domains without a documented mapping. A network-synchronized event is not proof of identical artistic interpretation or performer experience.

## 6. Local knowledge, authorship and consent

GENJE must not define one universal movement vocabulary for distinct communities, practices or genres. A movement term may be language-specific, lineage-specific, contested or meaningful only in a particular teaching/performance context.

For any field recording, notation project or archive:
- identify the work, practice, place and language as specifically as participants authorize;
- credit performers, choreographers, teachers, notators, musicians and collaborators according to their wishes;
- record the authority to consent and any collective/community protocols relevant to the work;
- agree on capture purpose, access, retention, derivative creation and publication separately;
- allow withdrawal or restricted access where agreed and legally feasible;
- distinguish public performance from permission to record, train a model on, remix or republish it;
- do not infer identity, emotion, health, personality, ability or intent from movement.

FAIR data principles do not override CARE principles, creator rights or community authority. An open technical format is not an open cultural licence.

## 7. First local experiment

A low-risk first experiment can use a founder-authored short GENJE phrase, a written movement description and a musical timing track. No camera or wearable is necessary.

1. Author and timestamp the phrase.
2. Record its musical/event timing.
3. Represent it in one selected notation/score form.
4. Manually compare the score with the authored phrase.
5. Exchange the timing through OSC or MIDI only if useful.
6. Document what was preserved, omitted and reinterpreted.

This tests the research workflow without turning a performer into a dataset or requiring a new motion-capture system.

## 8. References

- [Library of Congress Dance Notation Collection](https://tile.loc.gov/storage-services/service/gdc/gdcfindingaidpdfs/mu020028/mu020028.pdf).
- [Harvard Library performing-arts research guide](https://guides.library.harvard.edu/c.php?g=1294023&p=9509243).
- [Ohio State University Dance Notation resources](https://dance.osu.edu/research/dnb/resources).
- Watts (2015), [Benesh Movement Notation and Labanotation](https://doi.org/10.1080/01472526.2015.1085227).
- [CARE Principles for Indigenous Data Governance](https://doi.org/10.5334/dsj-2020-043).
- [UNESCO Ethical Principles for Safeguarding Intangible Cultural Heritage](https://ich.unesco.org/en/ethics-and-ich-00866).

**Maturity:** RESEARCH / PROPOSED VALIDATION. No empirical conversion, movement study, notation qualification or participant research is claimed.

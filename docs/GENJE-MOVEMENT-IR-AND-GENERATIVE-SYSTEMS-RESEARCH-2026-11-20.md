# GENJE — Movement Intelligence, Notation and Generative Systems Research

**Date:** 2026-11-20  
**Status:** RESEARCH / ARCHITECTURE PROPOSAL  
**Ownership:** GENJE owns movement, choreography, sound, creative authorship and performance context. FELOH Corpus owns shared evidence and navigation. IKAI owns participant-facing reflection and privacy. WARENA owns infrastructure, runtime, reproducibility and security.

> **Research conclusion:** GENJE should define and govern a human-readable, event-oriented Movement Intermediate Representation (Movement IR). Labanotation, Motif, Laban Movement Analysis, motion-capture formats, music-alignment systems and generative models should connect through explicit adapters. No single notation, dataset or model should become the authoritative representation of African movement or of a performer.

This document consolidates the LaMoGen paper and static source-code audit with comparative research into movement notation, music-conditioned dance generation, motion-language systems, motion capture, embodied knowledge and a proposed GENJE architecture. It is a research specification, not a claim that a movement engine, capture system, dataset or product exists.

## 1. Scope and research questions

The programme asks:

1. How can movement be described at several levels—from an authored choreographic phrase to a measured joint trajectory—without confusing those levels?
2. How can a representation preserve performer agency, improvisation, cultural context, authorship and variation?
3. How can movement events align with music, livecoded sound and visual events while keeping clock uncertainty explicit?
4. Which existing systems can be reused as adapters, comparators or isolated research tools?
5. What would a local-first, reproducible and libre-oriented authoring environment require?
6. How can movement be observed from video or motion capture without presenting machine inference as ground truth?

In scope: Labanotation / Kinetography Laban, Motif, LMA, Bartenieff-related movement study, symbolic and continuous motion representations, text-to-motion, motion-to-text, music-to-dance, motion-to-notation, human-authored scores, situated African movement documentation, synchronisation, provenance, consent and rights.

Out of scope: a universal notation for African movement; automated judgement, ranking, diagnosis, identity recognition or emotion/personality inference; unconsented capture; treating model output as human choreography; selecting a production model or runtime before qualification; treating public datasets as cleared training material without rights review.

## 2. Concepts that must remain distinct

| Concept | Meaning here | Not equivalent to |
|---|---|---|
| Choreography | Authored arrangement of movement, space, time, relation and performance choices | A skeleton sequence or model output |
| Movement notation | Symbolic convention for recording selected movement information | The movement itself |
| Labanotation / Kinetography Laban | Detailed score notation with body-part, direction, level, duration and other conventions | LMA or Motif |
| Motif | Selective, abstract notation of salient movement ideas | Full transcription |
| Laban Movement Analysis | Descriptive framework including Body, Effort, Space and Shape | Labanotation |
| Bartenieff Fundamentals | Related movement practice and developmental movement concepts | A synonym for LMA or notation |
| Kinematics | Measured/calculated position, orientation, velocity and acceleration | Intention, effort quality or meaning |
| Motion capture | Measurement process with a sensor, calibration and coordinate frame | A validated interpretation |
| Movement IR | Proposed GENJE interoperable data model with epistemic and provenance fields | A universal dance notation |
| Motion generation | Computational synthesis under specified conditions | Human choreographic authorship |

LMA's four broad components are commonly described as Body, Effort, Space and Shape. Effort factors are Weight, Time, Space and Flow, each with qualitative polarities. These are interpretive movement concepts; they must not be collapsed into simple sensor thresholds. A measured pelvis velocity is a kinematic feature, not by itself a complete Effort-Time or Effort-Weight judgement.

A 2019 LMA reliability study reported materially different inter-rater reliability across categories, including lower agreement for Effort and Shape than for some other categories. This is a methodological warning, not a universal verdict on LMA: the study's task, participants and coding context constrain generalisation. Preserve annotator, context, disagreement and uncertainty rather than inventing a single objective label.

## 3. LaMoGen / LabanLite — paper and implementation audit

### 3.1 Paper identity and contribution

Jiang, Au, Xiang and Chen, “LaMoGen: Language to Motion Generation Through LLM-Guided Symbolic Inference,” CVPR 2026, pp. 9364–9373.

- [arXiv paper](https://arxiv.org/abs/2603.11605)
- [CVPR paper PDF](https://openaccess.thecvf.com/content/CVPR2026/papers/Jiang_LaMoGen_Language_to_Motion_Generation_Through_LLM-Guided_Symbolic_Inference_CVPR_2026_paper.pdf)
- [Supplementary material](https://openaccess.thecvf.com/content/CVPR2026/supplemental/Jiang_LaMoGen_Language_to_CVPR_2026_supplemental.pdf)
- [Project repository](https://github.com/jjkislele/LaMoGen)

LaMoGen's central contribution is a symbolic bridge between natural-language descriptions and generated motion. It adapts a selected subset of Labanotation concepts into a computational representation called LabanLite, then uses retrieval and LLM-guided composition to condition motion generation.

Its research value for GENJE is the explicit symbolic intermediate layer. LabanLite is not full Labanotation, not LMA, not Bartenieff practice and not a complete account of choreography.

### 3.2 Pipeline

The conceptual pipeline is:

1. Motion-capture data is preprocessed into a HumanML3D-style representation.
2. A LabanLite extraction stage converts motion into discrete symbolic codes.
3. A codebook and conceptual descriptions provide a symbolic vocabulary.
4. Text descriptions are embedded for retrieval of related movement examples.
5. An LLM composes or refines symbolic descriptions using retrieved examples.
6. A symbolic parser and Laban generator/codec produce motion representations.

This is not simply “an LLM that dances.” It is a multi-stage pipeline involving data preprocessing, a discrete movement representation, retrieval, language-model composition and learned motion reconstruction/generation.

### 3.3 LabanLite representation

The reported codebook is 158-dimensional and allocates code ranges to body-part groups:

| Group | Code range |
|---|---:|
| Support-L | 0–22 |
| Support-R | 23–45 |
| Support-Both | 46–71 |
| Upper-L | 72–94 |
| Upper-R | 95–117 |
| Torso | 118–139 |
| Upper-L relative | 140–148 |
| Upper-R relative | 149–157 |

The representation uses conceptual attributes such as direction, level and hold, and more detailed attributes such as orientation, bend and moving-effort. Conceptual descriptions include a body-part group, a movement semantic and a duration.

This is useful for machine processing and controlled reconstruction, but it is a deliberately reduced vocabulary. It does not encode the full range of Labanotation symbols and conventions. Frame-wise quantisation also creates a different authoring experience from an event-oriented human score: compact phrases and performer-specific nuances can be lost when represented only as repeated discrete frame codes.

### 3.4 Dataset and benchmark limits

The paper reports this action distribution:

| Action | Samples |
|---|---:|
| Walk | 1,956 |
| Step | 320 |
| Jump | 194 |
| Run | 130 |
| Jog | 86 |
| Hop | 46 |
| Sprint | 8 |
| Leap | 4 |
| Skip | 4 |
| **Total** | **2,748** |

This is strongly locomotion-weighted. It is not a representative sample of dance, Genge, Turkana/Ateker movement, social dance, improvisation, partner work, group formation or ritual context. Do not use it as a proxy for GENJE's movement scope.

The paper's semantic, temporal and alignment metrics evaluate aspects of text-motion correspondence and temporal structure. They do not establish cultural validity, groove, syncopation, musical phrasing, performance quality, embodied intention or practitioner acceptance. The reported human assessment involved graduate-student participants and a limited selection of motion examples; it is not a broad evaluation by dancers, choreographers, notation specialists or the communities whose movement traditions might be documented.

### 3.5 Omitted or simplified areas

The demonstrated representation and experiments leave important areas outside their scope:

- Detailed finger, toe and facial movement.
- Rich performer-to-performer relationships and group formations.
- General object/prop interaction and complex stage relationships.
- Comprehensive musical structure, metre, swing, syncopation and phrase-level performance.
- A full LMA account of Effort, Shape and Body.
- Performer-specific style and the distinction between canonical action and individual variation.
- Cultural provenance, authorship, consent and recording/reuse restrictions.

The supplement discusses limitations of the reduced vocabulary and the possibility that quantisation maps different performers or styles to the same symbolic representation. GENJE should therefore retain source motion, performer variation and human correction as first-class records.

### 3.6 Source-code audit — static inspection only

The public repository was inspected at source level. This was not a clean installation, training run, inference run, benchmark reproduction or security audit.

Observed implementation characteristics and qualification questions:

- Python 3.10-era machine-learning stack, PyTorch / Lightning, CUDA-oriented dependencies, Transformers and CLIP-related retrieval components.
- Explicit CUDA device assumptions in portions of the code; CPU or other accelerator portability requires testing.
- An OpenAI-compatible client path with a configured external provider/model. API credentials passed as command-line arguments can be exposed through shell history or process inspection, depending on environment.
- External LLM processing creates a data-flow and privacy question if movement descriptions or participant information are sent to a provider.
- Pickle-based artefacts must be treated as trusted-only inputs; untrusted pickle loading can execute code.
- Dependency declarations and installation instructions require reconciliation before a reproducible environment can be claimed.
- Parsing, error handling, coordinate transforms and duration handling require dedicated tests before reuse.

These are source-review observations and qualification questions, not proof that every deployment is vulnerable or that the model cannot run. The code's MIT licence does not automatically grant rights to HumanML3D/AMASS-derived data, SMPL assets, checkpoints, third-party packages or media. Each artefact needs its own licence and terms review.

**GENJE disposition:** retain LaMoGen as a research comparator and possible isolated adapter. Do not adopt LabanLite as GENJE's canonical notation or make its Python/CUDA/external-LLM stack a WARENA runtime dependency.

## 4. Comparative movement and generation systems

These systems solve different problems. Their outputs and metrics are not directly comparable unless datasets, splits, representations and evaluation protocols match.

| System / line of work | Main contribution | GENJE relevance | Key caution |
|---|---|---|---|
| LaMoGen (CVPR 2026) | LLM-guided symbolic inference through LabanLite for text-to-motion | Symbolic bridge and retrieval/composition architecture | Reduced notation; locomotion-heavy benchmark; execution not reproduced |
| LLaMo (CVPR 2026) | Language-conditioned motion generation using continuous/autoregressive motion-token approaches | Counterpoint to discrete symbolic IR; streaming and motion-language interface research | Latent tokens are not a human-authored score or cultural ontology |
| LAMP (CVPR 2026) | LLM planning through a structured motion domain-specific language for 3D trajectories | Explicit, inspectable movement programs and constraints | Motion DSL is not automatically dance notation |
| FACT (ICCV 2021) | Music-conditioned 3D dance generation | Early audio-to-motion reference | Dataset and genre coverage constrain claims |
| AIST++ | Multi-view dance video, 3D pose and music-linked benchmark derived from AIST Dance DB | Multi-view pose, motion representation and music/motion alignment research | Not culturally representative of African dance |
| Bailando / EDGE / Lodge family | Music-to-dance generation using learned motion representations and structured generation | Comparative model families for rhythm and dance generation | Plausibility does not establish choreographic quality or cultural fit |
| FineDance (ICCV 2023) | Fine-grained music-to-dance dataset and generation benchmark | Dance/music research reference | Genres and capture conditions are bounded |
| ChoreDiffusion (2026) | Beat-aware diffusion for music-conditioned dance generation | Beat-conditioned synthesis and temporal evaluation | Cross-paper numbers are not controlled head-to-head comparisons |
| DanceLDM (2026) | Latent diffusion for music-conditioned dance generation/editing | Editing and latent-space comparison | Reproducibility and source revision require qualification |
| Motion-to-Labanotation research | BVH/MoCap-to-notation pipelines using segmentation and learned sequence models | Reverse-path research | Automated transcription is candidate annotation, not authoritative score |

### 4.1 AIST++ and dataset discipline

AIST++ provides 1,408 dance sequences across ten genres, paired music, multi-view recordings and 3D keypoints. It is useful for studying multi-view pose, motion representation and music-conditioned generation. Its benchmark design and train/test splits must be read carefully; different tasks use different splits and overlap controls.

AIST++ is not a representative African movement archive and must not be used as a stand-in for GENJE, Genge, Turkana or Ateker practice. Dataset annotations, source videos, original music and performer rights may have different terms. Check the dataset terms of use and attribution requirements before downloading, processing, redistributing or training on it.

### 4.2 Model-family comparison

The key distinction is not which model has the highest reported benchmark score. It is which representation and workflow best support human authorship:

- **Symbolic-first systems** such as LaMoGen offer interpretable intermediate structure, but their vocabulary may be narrow.
- **Continuous motion-token systems** such as LLaMo can preserve richer temporal detail, but latent tokens may be difficult for a choreographer to inspect or edit.
- **Motion DSL systems** such as LAMP make trajectories and constraints explicit, but need a separate semantic and cultural layer.
- **Diffusion systems** can produce diverse motion and support editing, but may be hard to reproduce, steer and audit at the level of an individual event.
- **Music-conditioned systems** model correlations between audio and movement; they do not prove that generated motion understands the cultural role of a rhythm or the intention of a performer.

A useful architecture can combine these strengths without making one model the source of truth.

## 5. GENJE Movement IR — proposed canonical representation

### 5.1 Design requirements

The proposed Movement IR should be:

1. **Human-readable:** a choreographer can inspect and author it without a trained model.
2. **Event-oriented:** movement phrases and events are primary; frame samples are derived execution data.
3. **Plural:** it can express different bodies, practices, vocabularies and levels of detail without forcing one taxonomy.
4. **Layered:** authored description, notation, measurement, inference and interpretation are separately represented.
5. **Time-aware:** events can align to beats, bars, phrases, clocks and uncertain timing.
6. **Spatially explicit:** local body coordinates and global stage coordinates are distinct; formations and object relations are representable.
7. **Provenance-bearing:** every annotation has an author/source, method, version, date and uncertainty context.
8. **Reversible where possible:** adapters declare information they lose, transform or cannot represent.
9. **Local-first:** authoring and inspection do not require cloud inference or a hosted account.
10. **Culturally accountable:** community terms, restrictions and alternate readings can be preserved without universalising them.

### 5.2 Core layers

| Layer | Contents | Example |
|---|---|---|
| Work | Work/session identity, creator, collaborators, context, rights | Named choreography or rehearsal |
| Score | Human-authored phrase and event sequence | “Two steps, pause, shoulder-led turn” |
| Body | Body-part/group references and relations | Left support, right arm, torso |
| Space | Direction, level, pathway, orientation, stage region, formation | Travel diagonally downstage |
| Time | Duration, onset, beat/bar/phrase relation, tempo map | Event starts on beat 3 |
| Dynamics | Qualitative movement description and measured kinetics, kept distinct | “Sustained” annotation vs measured velocity |
| Sound | Music source, meter, beat grid, cue, livecoding event | Sound event E-42 aligns to phrase P-3 |
| Relation | Performer-to-performer, performer-to-object and group relations | Mirrored pair; object hand-off |
| Observation | Capture source, sensor, coordinate frame, sampling and missingness | Multi-view pose estimate |
| Interpretation | Human annotation, cultural explanation, uncertainty and disagreement | Performer-authored explanation |
| Provenance | Who authored, observed, measured, inferred, reviewed or changed each field | Annotator and source record |
| Rights / consent | Permission, access, retention, publication and deletion constraints | Private rehearsal; no public video |

### 5.3 Epistemic status

Every meaningful value or annotation should identify how it is known. Proposed vocabulary:

- **AUTHORED** — deliberately composed or entered by a human creator.
- **OBSERVED** — directly observed and recorded by a named observer.
- **MEASURED** — produced by a specified instrument or calculation.
- **INFERRED** — estimated by an algorithm or derived from other values.
- **INTERPRETED** — a human reading or analysis, not direct measurement.
- **COMMUNITY_ATTESTED** — reviewed or affirmed through an explicitly documented community process.
- **UNKNOWN** — source or epistemic basis is not known.

These labels are not quality rankings. An inferred value is not automatically inferior for every task, but it must never be silently relabelled as observed or authored. Preserve disagreement and alternative readings.

### 5.4 Time and music alignment

Movement time needs more than a floating-point timestamp. Support:

- Absolute session time with clock identity.
- Event-relative time and duration.
- Musical position (bar, beat, subdivision).
- Tempo maps and tempo changes.
- Phrase and section labels.
- Swing, syncopation and microtiming annotations where relevant.
- Uncertainty and clock-offset estimates.
- Explicit mapping between audio, display, capture and movement clocks.

A shared event ID may connect a movement cue to a musical event. It must not imply that sound caused movement or that movement has one correct musical interpretation.

### 5.5 Spatial model

Maintain separate coordinate spaces:

- **Body-local:** relative to a body segment or performer.
- **Performer/world:** performer placement in the shared environment.
- **Stage/world:** stage, room or capture-volume coordinates.
- **Object-local:** relative to a prop or external object.

Each transform needs a declared convention, units, handedness, origin, calibration and version. Group choreography needs relations and formations, not merely independent skeleton tracks. A canonicalised skeleton can aid comparison but must not erase original stage placement or partner relations.

### 5.6 Interchange and adapters

Movement IR is the canonical GENJE model. Adapters may include:

- Labanotation / Kinetography Laban.
- Motif notation.
- LMA and Bartenieff-informed annotation, with qualified human practitioners.
- BVH and other motion-capture skeleton formats.
- HumanML3D-like representations.
- LaMoGen LabanLite.
- Motion DSLs such as LAMP's approach.
- Music cue/event formats and livecoding logs.
- Video-derived pose tracks, only as inferred observation data.

Every adapter must publish a mapping table and loss report: supported fields, approximations, omitted concepts, coordinate changes, temporal quantisation and required human review. No adapter silently becomes canonical.

## 6. Observation and reverse transcription

LaMoGen is text-to-motion; it does not solve the reverse problem of turning arbitrary camera footage into a trustworthy movement score.

A separate candidate pipeline is required:

**Video / MoCap → capture calibration → pose or skeleton estimation → kinematic features → candidate event segmentation → candidate notation mapping → human review → approved score**

Each stage introduces uncertainty. Camera angle, occlusion, clothing, lighting, body proportions, frame rate, camera calibration, skeleton definition and missing joints affect results. Pose estimation does not establish intention, cultural meaning or a correct choreographic description.

Required controls:

- Capture only with explicit, purpose-specific consent.
- Prefer synthetic or already-cleared data during early engineering.
- Keep raw video and derived pose data separate, with different access and retention.
- Preserve original media provenance and transformations.
- Mark all machine-derived values INFERRED.
- Let performers and qualified practitioners correct, reject or remove annotations.
- Never infer health, emotion, identity, personality, skill or intent.
- Do not use a confidence score as a substitute for human review.
- Record calibration, coordinate frame, sampling, dropped frames and uncertainty.

## 7. African-centred and situated movement documentation

GENJE should not treat “African dance” as one style or a single dataset category. African movement practices are plural, historically situated and connected to language, music, social roles, place, age, spirituality, labour, celebration, politics and everyday life in different ways.

Existing research leads:

- Latipher Amma Osei (2020), **“Documenting Ghanaian dances through Labanotation,”** *African Research Review* 14(2), 112–120. Considers Labanotation as a documentation resource and discusses challenges and possible use of cinematography. It is a situated Ghanaian case, not a universal method. [University of Education, Winneba record](https://www.uew.edu.gh/theatre-arts/staff/laosei/publications/29001/detail).
- Felix Akinsipe (2015), **“Development of ‘Stick Figure’ Notation for African Dances.”** Treat as a proposal requiring full-text review and critical assessment, not an established consensus or validated replacement.
- Grim-Feinberg and Wong Santos, **“Movement Notation and the Analysis of Embodied Knowledge: Three Ethnographic Examples.”** A methodological reference for practitioner correction and multi-modal documentation. [Journal article](https://jashm.press.uillinois.edu/22.2/grim-feinberg.html).
- The Dance Notation Bureau archival record for Odette Blum's *African Dances and Games* illustrates a historical combination of dance description, cultural/historical background, rhythm, film and Labanotation. Archival access does not grant permission to reproduce restricted scores or media.

### 7.1 Proposed plural documentation bundle

A practitioner-led record may combine, where appropriate:

1. The practitioner's own description and terminology.
2. Demonstration, teaching and embodied learning context.
3. Audio and rhythm documentation.
4. Video or stills only with appropriate consent and access restrictions.
5. A notation selected for the actual question.
6. Variation and improvisation notes.
7. Historical, linguistic, social and place context.
8. Multiple interpretations and practitioner corrections.
9. Credits, authorship, rights, access and preservation instructions.
10. Community review and a documented route to correction or withdrawal.

The method must be selected with practitioners and relevant communities, not imposed by software architecture. Do not label an individual or community as a source of generic “African movement data.” A score is a situated representation of selected aspects of movement, not the movement or its community.

### 7.2 Research gaps and next evidence

This research pass did not establish a comprehensive, community-governed African dance benchmark covering the diversity GENJE is concerned with. This is a bounded finding about this research pass, not a claim that no such archive, project or dataset exists.

Before any Turkana/Ateker-specific study, identify local practitioners, language and terminology, permissions, ownership expectations, restrictions, community benefits and whether documentation is wanted at all. Do not invent tradition-specific vocabulary.

## 8. Technical architecture and WARENA compatibility

### 8.1 Proposed research stack

| Concern | Candidate | Role / disposition |
|---|---|---|
| Human authoring | Emacs / Org-mode | Human-readable score, notes and research records |
| Canonical transforms | Guile / Scheme | Candidate implementation language for Movement IR and adapters |
| Local records | SQLite | Searchable local metadata and event records |
| Reproducibility | GNU Guix | Pinned environments, package provenance and build records |
| Service supervision | GNU Shepherd | Only if a persistent local service is justified |
| Audio synthesis | SuperCollider | Sound engine candidate; preserve patch and routing provenance |
| Algorithmic music | TidalCycles | Rhythm/pattern authoring candidate; record exact runtime and integration |
| Visual / 3D inspection | Blender | Offline visualisation and interchange test candidate |
| Motion capture | BVH and other open/interchange formats | Adapter boundary; qualify each format and tool |
| Generative research | LaMoGen and comparators | Isolated adapters / experiments, not canonical runtime |
| XR | Native OpenXR / qualified runtime | Later stage; WARENA owns infrastructure, IKAI owns participant experience |

This is a research disposition, not a declaration that packages are installed, integrated or selected for production.

### 8.2 Technology policy

Follow WARENA's native-first, libre-first, local-first and reproducibility policy. JavaScript is excluded as a runtime, application language, framework or architectural dependency. Browser-based systems may be studied as external references but must not silently become the GENJE/WARENA application substrate.

Python-based research systems may run in an isolated, pinned compatibility environment when justified. Their use does not make Python the canonical Movement IR language or require adoption of CUDA, hosted LLMs or cloud services. External model calls require separate data-flow, consent, retention and provider review.

### 8.3 Logical architecture

    Human author / practitioner
              |
              v
    GENJE Movement IR  <---->  Org / score authoring
              |
              +---- notation adapters (Labanotation, Motif, LMA annotations)
              |
              +---- observation adapters (BVH, MoCap, inferred pose)
              |
              +---- music/event adapters (tempo, beats, cues, livecoding)
              |
              +---- generation adapters (LaMoGen, LLaMo, LAMP, diffusion)
              |
              +---- execution / inspection (Blender, later XR)
              |
              v
    Provenance, rights, consent, loss reports and human review

    WARENA: local runtime, packaging, security and reproducibility
    IKAI: participant-facing reflection, privacy and control
    FELOH Corpus: shared governance, evidence and cross-project index

## 9. Evaluation framework

Do not reduce evaluation to one score. Use separate dimensions:

| Dimension | Example evidence |
|---|---|
| Notation fidelity | Qualified practitioner review; round-trip score inspection |
| Temporal fidelity | Beat/phrase alignment error with clock uncertainty |
| Spatial fidelity | Coordinate-frame tests, path and formation comparison |
| Kinematic fidelity | Joint/trajectory error under declared skeleton and calibration |
| Choreographic usefulness | Dancer/choreographer assessment in the actual creative task |
| Expressive range | Variation, improvisation and style-preservation review |
| Cultural validity | Practitioner/community review and correction rights |
| Interpretability | Ability to inspect and edit symbolic/event representation |
| Reproducibility | Pinned source, environment, assets, commands and repeatable output |
| Privacy and consent | Demonstrated capture controls, access, export/delete and retention |
| Interoperability | Adapter tests and explicit transformation-loss reports |

FID, diversity, beat alignment or retrieval similarity can be useful within a defined experimental protocol. They do not independently measure cultural validity, authorship, musical meaning or choreographic quality.

## 10. Staged research roadmap

| Stage | Work | Exit evidence |
|---|---|---|
| R0 — Evidence | Verify papers, datasets, licences, code revisions and existing GENJE records | Annotated source register and claim/evidence matrix |
| R1 — Movement IR | Define event schema, identity, time, space, epistemic status and provenance | Reviewed specification and example authored scores |
| R2 — Manual authoring | Create scores without AI or sensing | Practitioner can author, revise and export |
| R3 — Notation adapters | Map selected Labanotation/Motif/LMA fields | Mapping tests and explicit loss reports |
| R4 — Music alignment | Connect movement events to beat/bar/phrase and livecoding cues | Clock-domain and alignment tests |
| R5 — 3D inspection | Export controlled examples to Blender or qualified viewer | Coordinate and reconstruction tests |
| R6 — Observation | Evaluate MoCap/video-to-candidate-notation with consent and human review | Calibration, uncertainty and correction evidence |
| R7 — Generative comparison | Compare symbolic, continuous, DSL and diffusion approaches | Reproducible experiments; human evaluation |
| R8 — Situated practice | Co-design a locally grounded process with practitioners | Consent, governance, terminology and community review |
| R9 — XR / embodied interface | Consider spatial interaction only after prior stages justify it | Device, privacy, latency and accessibility qualification |

### Acceptance criteria before a prototype is called a GENJE Movement system

- A person can author and revise a score without a model.
- The representation distinguishes authored, observed, measured, inferred and interpreted information.
- Every adapter declares omissions and transformation losses.
- Musical alignment supports tempo changes and clock uncertainty.
- Group, stage and object relationships are not erased by body normalisation.
- Performer and practitioner corrections are retained as provenance.
- Cultural terms are attributed and not universalised.
- Dataset, model, code, media and performer rights are recorded separately.
- Offline operation and reproducible environments are demonstrated where claimed.
- No diagnosis, identity recognition, hidden profiling or performer ranking is present.

## 11. Decisions and current dispositions

| Topic | Disposition |
|---|---|
| Canonical movement representation | **PROPOSED:** GENJE Movement IR; human-authored and event-oriented |
| LaMoGen / LabanLite | **RESEARCH ADAPTER:** symbolic inference comparator; not canonical notation |
| LMA / Labanotation / Motif | **PLURAL METHODS:** distinct traditions and adapters; practitioner expertise required |
| Motion capture and pose estimation | **LATER RESEARCH:** only for a defined question, with consent and uncertainty |
| Music-to-dance models | **COMPARATIVE RESEARCH:** not selected as choreographic authority |
| Python/CUDA model stack | **ISOLATED COMPATIBILITY:** not WARENA's canonical runtime |
| Cloud LLM processing | **NOT DEFAULT:** separate opt-in and data-flow review required |
| African movement dataset | **NO UNIVERSAL DATASET CLAIM:** practitioner-led, situated documentation preferred |
| Product / deployment | **NOT CLAIMED:** research and specification only |

## 12. Existing GENJE records and ownership

This specification extends rather than replaces:

- [Labanotation and Movement-Score Research](LABANOTATION-MOVEMENT-SCORE-RESEARCH-2026-11.md)
- [Kinetics, Livecoding & Reflective Interaction](KINETICS-LIVECODING-AND-IKAI-INTERACTION-2026-11-18.md)
- [Embodied Spatial Interaction Research](EMBODIED-SPATIAL-INTERACTION-RESEARCH-2026-11-14.md)

Detailed movement and creative research belongs to GENJE. IKAI may use participant-directed reflection but does not own choreography or movement interpretation. WARENA provides qualified infrastructure, not cultural semantics. FELOH Corpus records shared boundaries and links to the specialist source.

## 13. References and source trail

### Primary papers and project sources

- Jiang, J., Au, H. Y., Xiang, J. & Chen, J. (2026). “LaMoGen: Language to Motion Generation Through LLM-Guided Symbolic Inference.” CVPR 2026, 9364–9373. [arXiv](https://arxiv.org/abs/2603.11605) · [CVF paper](https://openaccess.thecvf.com/content/CVPR2026/papers/Jiang_LaMoGen_Language_to_Motion_Generation_Through_LLM-Guided_Symbolic_Inference_CVPR_2026_paper.pdf) · [Supplement](https://openaccess.thecvf.com/content/CVPR2026/supplemental/Jiang_LaMoGen_Language_to_CVPR_2026_supplemental.pdf) · [Code](https://github.com/jjkislele/LaMoGen).
- [LaMoGen project page](https://jjkislele.github.io/LaMoGen/).
- [CVPR 2026 proceedings](https://openaccess.thecvf.com/CVPR2026) — LLaMo and LAMP paper records; verify exact paper/version before reproducing claims.
- [AIST++ dataset and project documentation](https://google.github.io/aistplusplus_dataset/).
- Li et al. (2021). “FACT: Learning to Generate 3D Dance Motions with Feature Matching.” ICCV 2021. [CVF proceedings](https://openaccess.thecvf.com/ICCV2021).
- Li et al. (2023). “FineDance: A Fine-grained Dance Dataset for Music-to-Dance Generation.” ICCV 2023. [CVF proceedings](https://openaccess.thecvf.com/ICCV2023).
- [ChoreDiffusion discovery record](https://arxiv.org/search/?query=ChoreDiffusion&searchtype=all).
- [DanceLDM discovery record](https://arxiv.org/search/?query=DanceLDM&searchtype=all).
- [LabanFormer discovery record](https://scholar.google.com/scholar?q=LabanFormer+2023).
- [IEEE Access — Labanotation generation from dance movement](https://ieeexplore.ieee.org/search/searchresult.jsp?queryText=Labanotation%20generation%20dance%20movement).
- [IEEE ICME — end-to-end Labanotation generation from motion capture](https://ieeexplore.ieee.org/search/searchresult.jsp?queryText=end-to-end%20Labanotation%20motion%20capture).

### Movement analysis and notation

- [NYU Movement Research Group](https://movementresearch.org/).
- [Frontiers — Laban Movement Analysis research](https://www.frontiersin.org/).
- [PLOS ONE — “Assessing the reliability of the Laban Movement Analysis system”](https://journals.plos.org/plosone/).
- [International Council of Kinetography Laban](https://ickl.org/).
- [Dance Notation Bureau](https://dancenotation.org/).
- [Ohio State University — Dance Notation resources](https://dance.osu.edu/research/dnb/resources).
- Osei, L. A. (2020). “Documenting Ghanaian dances through Labanotation.” *African Research Review*, 14(2), 112–120. [University of Education, Winneba record](https://www.uew.edu.gh/theatre-arts/staff/laosei/publications/29001/detail).
- Akinsipe, F. (2015). “Development of ‘Stick Figure’ Notation for African Dances.” Full-text review and bibliographic verification remain required.
- Grim-Feinberg & Wong Santos, “Movement Notation and the Analysis of Embodied Knowledge: Three Ethnographic Examples.” [Journal article](https://jashm.press.uillinois.edu/22.2/grim-feinberg.html).

### Research and reproducibility note

Some links above are project portals, search records or journal landing pages rather than the exact versioned paper or source revision. They are discovery/navigation leads, not substitutes for a source-register entry containing exact bibliographic metadata, passages, version, access date and licence. The LaMoGen repository review was static inspection only; no environment build, model execution, benchmark reproduction, vulnerability scan or full dataset-rights audit was performed.

**Final position:** GENJE Movement IR → notation, observation, musical and generative adapters → practitioner-authored creative practice. The representation serves the dancer, choreographer and community; it does not replace them.

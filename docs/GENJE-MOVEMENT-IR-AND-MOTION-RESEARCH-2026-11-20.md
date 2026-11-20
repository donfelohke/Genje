# GENJE — Movement Intermediate Representation and Motion Research

**Date:** 2026-11-20  
**Status:** RESEARCH / ARCHITECTURE PROPOSAL  
**Owner:** GENJE — movement, choreography, sound, performance and embodied creative practice  
**Related domains:** FELOH Corpus — shared evidence and provenance; IKAI — participant-directed reflection; WARENA — reproducible infrastructure  
**Implementation status:** No GENJE Movement IR, motion-capture pipeline, choreography engine or model integration is claimed as implemented.

## 1. Executive position

GENJE should develop an independent, human-authored **Movement Intermediate Representation (Movement IR)** rather than adopting LaMoGen/LabanLite, a motion-generation model, a dataset schema or a single notation system as its canonical language.

The Movement IR is a proposed semantic and temporal layer connecting distinct artefacts:

1. authored choreography and movement scores;
2. established notation systems and movement-analysis vocabularies;
3. music, rhythm and performance timing;
4. observed or measured motion;
5. rendered animation and generated motion;
6. contextual, cultural and provenance records.

These artefacts must remain distinguishable. A score is not a sensor measurement; a measurement is not an interpretation; a generated motion sequence is not an authored cultural account. Adapters may translate between them, but every translation must disclose its assumptions, uncertainty and information loss.

**Recommended architecture:**

`Human-authored Movement IR → notation / music / observation / generation / rendering adapters → performer-reviewed practice`

The initial system is text- and score-first. Camera, wearable, XR and model-based pathways are later optional research tracks, not prerequisites.

## 2. Research question and scope

**Primary question:** How can GENJE represent, compare, compose and revisit movement in relation to sound, space, time and other performers while preserving authorship, cultural specificity, consent and interpretive openness?

In scope:
- movement events, phrases, stillness, transitions and repetition;
- body-part participation and articulation;
- local-body and global-stage spatial relations;
- timing, rhythm, meter, beat, subdivision, swing and phrase alignment;
- qualitative movement vocabularies, including LMA where appropriately taught and attributed;
- individual and group choreography, formations and performer-to-performer relations;
- links to music, livecoding, audiovisual systems and performance records;
- observation and generation as explicitly labelled, reviewable adapters.

Out of scope for the initial specification:
- biometric identity, person recognition or persistent body profiles;
- emotion, health, personality, intention or ability inference;
- performer ranking, normative scoring or automated artistic judgement;
- a universal African movement grammar;
- replacement of practitioner knowledge or community authority with model output;
- autonomous publication or release of generated choreography.

## 3. Conceptual distinctions

| Artefact or discipline | What it represents | What it does not establish |
|---|---|---|
| Choreographic score | An authored instruction, proposal or arrangement | That it was performed exactly as written |
| Labanotation / Kinetography Laban | Detailed symbolic notation for movement | Complete cultural meaning or lived context |
| Motif notation | Selective representation of salient movement ideas | Full transcription |
| Laban Movement Analysis (LMA) | A framework for observing Body, Effort, Space and Shape | A universal objective label set or diagnosis |
| Bartenieff Fundamentals | A related movement practice and developmental framework | A synonym for Labanotation or LMA |
| Kinematic measurement | Measured position, orientation, velocity or acceleration | Intention, emotion or stylistic meaning |
| Motion capture / pose estimation | An estimated or recorded representation of body configuration | Ground truth without calibration and validation |
| Motion generation | A model-produced or algorithmically composed sequence | Human authorship, cultural validity or performance quality |
| Music-to-dance alignment | A relation between audio structure and movement timing | That movement is musically or artistically successful |

Do not use “Laban” as a generic label for all of these. Preserve the name, version, teaching lineage and scope of each vocabulary or notation method.

## 4. LaMoGen / LabanLite audit

### 4.1 Research identity

Junkun Jiang, Ho Yin Au, Jingyu Xiang and Jie Chen, **“LaMoGen: Language to Motion Generation Through LLM-Guided Symbolic Inference,”** CVPR 2026, pp. 9364–9373.

- [arXiv paper](https://arxiv.org/abs/2603.11605)
- [CVPR paper](https://openaccess.thecvf.com/content/CVPR2026/papers/Jiang_LaMoGen_Language_to_Motion_Generation_Through_LLM-Guided_Symbolic_Inference_CVPR_2026_paper.pdf)
- [Supplementary material](https://openaccess.thecvf.com/content/CVPR2026/supplemental/Jiang_LaMoGen_Language_to_CVPR_2026_supplemental.pdf)
- [Project repository](https://github.com/jjkislele/LaMoGen)

LaMoGen's useful contribution is an intermediate symbolic representation between natural-language descriptions and generated motion. It is a research system and adapter candidate, not GENJE's canonical ontology.

### 4.2 Pipeline and representation

The published pipeline can be summarised as:

`text prompt → LLM-guided LabanLite composition → symbolic motion sequence → Laban Generator / Codec → motion features`

The research workflow also includes motion-capture preprocessing, HumanML3D-derived data, LabanLite extraction, a codebook, conceptual descriptions, CLIP-based retrieval and language-model composition.

LabanLite divides body groups into Support-L, Support-R, Support-Both, Upper-L, Upper-R and Torso, with relative upper-body groups. Its 158-dimensional codebook allocates:
- Support-L: 0–22
- Support-R: 23–45
- Support-Both: 46–71
- Upper-L: 72–94
- Upper-R: 95–117
- Torso: 118–139
- Upper-L relative: 140–148
- Upper-R relative: 149–157

Its conceptual descriptions encode body-part groups, semantic movement and duration. This compact representation can support retrieval and generation, but the frame-oriented codebook is not equivalent to the full event and phrase semantics required for choreography authoring.

### 4.3 Limits relevant to GENJE

- **Not full Labanotation:** LabanLite is a computational adaptation, not a complete implementation of Kinetography Laban.
- **Not full LMA:** Its moving-effort implementation is not equivalent to the four LMA Effort factors—Weight, Time, Space and Flow—and their qualitative poles.
- **Body coverage:** The paper's representation has limited skeletal/body-part coverage, including omissions of detailed finger and facial movement.
- **Spatial context:** Canonical skeleton normalisation and representation choices limit stage-coordinate, prop, object and multi-performer relationships.
- **Style and identity:** Quantisation can map different performers or stylistic variants to similar codes; the supplement acknowledges residual personal style is not fully represented.
- **Dataset balance:** The reported 2,748-example action distribution is heavily locomotion-oriented: Walk 1,956; Step 320; Jump 194; Run 130; Jog 86; Hop 46; Sprint 8; Leap 4; Skip 4. It is not a representative corpus of dance, improvisation or African movement practice.
- **Evaluation:** Semantic, temporal and alignment metrics do not establish groove, syncopation, embodied coordination, cultural validity, practitioner acceptance or choreographic quality.
- **Human evaluation:** The reported study involved 35 graduate students and selected motion examples; it is not a practitioner/community validation study.
- **Directionality:** LaMoGen is text-to-motion. Camera/MoCap-to-notation is a separate inverse problem requiring tracking, coordinate calibration, segmentation, uncertainty handling and human review.

### 4.4 Static implementation audit

The public repository was inspected at source level; this was not an installation or execution test.

The inspected stack includes Python 3.10, PyTorch 2.1.2, PyTorch Lightning 2.1.2, CUDA 11.8, NumPy 1.23.2, SMPL-X, Transformers 4.28.0 and OpenAI CLIP. The code has CUDA-specific assumptions, incomplete dependency declaration, an OpenAI-compatible external LLM client, and use of Python pickle. The LLM utility passes its API key as a command-line argument, which can expose secrets through shell history or process inspection depending on the environment. Coordinate transforms and parser/error-handling behaviour need explicit contracts and tests.

**Audit classification:** source-inspected; execution-unverified. No environment installation, inference, training, benchmark reproduction, GPU profiling, security scan or complete upstream dataset/asset licence audit was performed. The repository's MIT licence does not automatically license third-party datasets, models, checkpoints, SMPL assets or dependencies.

**WARENA compatibility:** retain LaMoGen only as an isolated research adapter if needed. Its Python/PyTorch/CUDA/LLM dependencies do not become the canonical GENJE or WARENA runtime. Do not transmit participant movement data to an external model provider by default.

## 5. Comparative motion research

The following projects represent different technical approaches. Their published metrics and datasets are not necessarily directly comparable; do not treat cross-paper leaderboard values as a controlled head-to-head evaluation.

| System / line | Contribution | GENJE research use | Main caution |
|---|---|---|---|
| **LaMoGen** (CVPR 2026) | LLM-guided symbolic LabanLite composition for text-to-motion | Symbolic intermediate-representation case study | Locomotion-heavy data; partial movement vocabulary and body coverage |
| **LLaMo** (CVPR 2026) | Continuous autoregressive motion tokens, mixture-of-transformers and flow-matching generation | Counterpoint to discrete symbolic tokens; streaming generation study | Generated continuity is not equivalent to interpretable choreography |
| **LAMP** (CVPR 2026) | LLM planning through a structured motion DSL and explicit 3D trajectories | Motion-program / DSL design reference | A DSL still needs human-authored semantics, provenance and cultural scope |
| **FACT** (ICCV 2021) | Music-conditioned 3D dance generation | Early music-to-motion architecture comparator | Dataset and style coverage constrain generalisation |
| **AIST++** | Paired music and multi-view dance motion data | Benchmark and data-engineering reference | Not a culturally representative African movement dataset |
| **FineDance** (ICCV 2023) | Fine-grained music/dance benchmark and generation research | More detailed dance-motion comparator | Dataset provenance, genre coverage and rights must be checked |
| **ChoreDiffusion** (2026) | Beat-aware diffusion-based dance generation | Beat-conditioned generation comparator | Beat alignment is not complete musicality or choreographic intent |
| **DanceLDM** (2026) | Latent diffusion for music/text-conditioned dance generation and editing | Editing and conditioning research | Model output remains generated material requiring author review |
| **Labanotation-from-MoCap studies** | Convert tracked motion into notation using segmentation, kinematic features and sequence models | Reverse-direction research | Automated transcription is a candidate score, not authoritative notation |

Key research references:
- [LLaMo — CVPR 2026](https://openaccess.thecvf.com/content/CVPR2026/html/Li_LLaMo_Scaling_Pretrained_Language_Models_for_Unified_Motion_Understanding_and_CVPR_2026_paper.html)
- [LAMP — CVPR 2026](https://openaccess.thecvf.com/content/CVPR2026/html/Kizil_LAMP_Language-Assisted_Motion_Planning_for_Controllable_Video_Generation_CVPR_2026_paper.html)
- [FACT / AI Choreographer — ICCV 2021](https://openaccess.thecvf.com/content/ICCV2021/html/Li_AI_Choreographer_Music_Conditioned_3D_Dance_Generation_With_AIST_ICCV_2021_paper.html)
- [AIST++ project and dataset documentation](https://google.github.io/aistplusplus_dataset/)
- [FineDance — ICCV 2023](https://openaccess.thecvf.com/content/ICCV2023/html/FineDance)
- [DanceLDM (2026)](https://doi.org/10.1007/s00530-026-02311-z)
- [Labanotation generation from motion capture — IEEE Access (2021)](https://ieeexplore.ieee.org/search/searchresult.jsp?queryText=The%20Method%20of%20Dance%20Movement%20Segmentation%20and%20Labanotation%20Generation%20Based%20on%20Rhythm)
- [End-to-end Labanotation generation from continuous motion capture — IEEE ICME (2020)](https://ieeexplore.ieee.org/search/searchresult.jsp?queryText=end-to-end%20Labanotation%20generation)
- [LabanFormer (2023)](https://arxiv.org/search/?query=LabanFormer&searchtype=all)

AIST++ documentation describes 1,408 sequences across ten dance genres, with paired music, 10.1 million frames/keypoints, 30 subjects and nine camera views. Its annotations and source media have distinct terms; read the dataset terms before reuse. AIST++ is useful as a technical benchmark, not as a proxy for GENJE's Genge, Turkana, Ateker or other African-centred practice.

## 6. Movement IR — proposed canonical model

The Movement IR should be a semantic event model with explicit time, space, body, relation and provenance. It should support both concise event scores and links to higher-resolution measured or generated streams.

### 6.1 Core entities

| Entity | Purpose |
|---|---|
| Work | Stable creative work identity, authorship, status and rights |
| Session | Rehearsal, research, performance or observation context |
| Performer | A participant reference controlled by the record's privacy policy; not a biometric identity |
| Phrase | A choreographic or musical grouping of events |
| Event | A movement action, stillness, transition or relation over an interval |
| Body map | Named body-part vocabulary and coordinate convention |
| Space frame | Local body, stage/world or explicitly defined reference frame |
| Relation | Relation between performer, performer, prop, object, group or spatial marker |
| Music map | Tempo/meter/beat/phrase references and clock-domain mapping |
| Annotation | Human-authored or attributed descriptive/interpretive statement |
| Evidence | Media, notation, measurement, source or testimony linked to the record |
| Transformation | Adapter operation, version, parameters, assumptions and loss report |

### 6.2 Event fields

A first schema should include:
- stable event ID and parent work/session/phrase IDs;
- start and end time, duration and timing confidence;
- body-part or body-group references;
- action/event type: move, hold, transition, repeat, contact, formation change or unknown;
- direction, level, orientation, pathway and spatial frame where relevant;
- local-body and global-stage coordinates as separate values;
- qualitative descriptors with vocabulary and author/source;
- measured kinematics in a separate measurement field;
- music references: beat, bar, subdivision, phrase and clock mapping;
- performer/prop/group relations;
- author, annotator, source, timestamp and revision history;
- epistemic status and uncertainty;
- consent, access, retention and rights metadata.

Avoid a single overloaded “effort” or “style” field. Preserve the original term, vocabulary version, author and explanatory context.

### 6.3 Epistemic status

Every annotation or value should identify how it is known. Proposed controlled labels:

- `AUTHORED` — supplied as an instruction or creative choice by an author.
- `OBSERVED` — described by a named observer in a stated context.
- `MEASURED` — produced by a stated measurement process and instrument.
- `INFERRED` — derived by a documented algorithm or reasoning step.
- `INTERPRETED` — an attributed reading or analysis, not a raw observation.
- `COMMUNITY_ATTESTED` — reviewed or affirmed through a documented community process.
- `UNKNOWN` — not established.

These labels are not a hierarchy of truth. A measured value can be wrong; a practitioner's interpretation can be authoritative for their own experience; community review must identify who participated and what authority they exercised.

### 6.4 Time and music

Movement time must not be reduced to a single frame rate or BPM value. Support:
- absolute session time and relative phrase time;
- beat/bar/subdivision references;
- meter, tempo changes and tempo maps;
- swing, syncopation, polyrhythm and deliberate displacement;
- phrase boundaries, pickup, anticipation, suspension and silence;
- audio clock, motion clock and display clock with explicit offset, drift and uncertainty.

A beat-synchronous score is one possible relation, not a requirement that every gesture land on a beat. Musical structure and choreographic interpretation remain separately authored.

### 6.5 Space and relations

Represent local-body coordinates separately from stage/world coordinates. Declare axis orientation, units, origin, handedness, calibration and transform history. Support pathways, facing, level, formations, interpersonal distance, contact and prop/object relations. Do not discard stage context through canonical skeleton normalisation.

### 6.6 Transformation contract

Every adapter must report:
1. source and target schema/version;
2. input provenance and rights;
3. assumptions and coordinate/time conventions;
4. mappings applied and values omitted;
5. uncertainty introduced or propagated;
6. lossy fields and unsupported concepts;
7. software version, parameters and reproducibility data;
8. human review and correction history.

Never silently convert a qualitative descriptor into a numeric score or a measured velocity into a claim about expressive effort.

## 7. Research and implementation stack

The stack is a proposal, not a declaration of installed components.

| Layer | Candidate | Role / boundary |
|---|---|---|
| Authoring | Emacs + Org-mode | Human-readable score, research notebook and versioned annotation |
| Canonical transforms | Guile / Scheme | Typed records, transformations and validation |
| Local store | SQLite | Local structured records and provenance links |
| Environment | GNU Guix | Pinned, reproducible development and evaluation environment |
| Service supervision | Shepherd | Only if a persistent local service is later justified |
| Audio / rhythm | SuperCollider; TidalCycles | Sound synthesis and pattern-driven performance |
| Visual inspection | Blender | Offline skeleton, trajectory and animation inspection |
| Model adapter | LaMoGen / selected motion models | Isolated interoperability experiments; not canonical runtime |
| Observation adapter | Manual annotation first; later optional MoCap/pose estimation | Candidate observations with calibration and uncertainty |
| Immersive output | OpenXR / native Linux runtime research | Later optional display and rehearsal output |

Python may be retained as a compatibility boundary for upstream research models. It must not become a hidden requirement of the canonical Movement IR or the WARENA runtime. Respect the existing WARENA native-first, libre-first, local-first policy and JavaScript/web-runtime exclusion.

## 8. Observation is a separate inverse pipeline

LaMoGen's text-to-motion direction does not solve camera-to-score. A future observation path would be:

`camera / MoCap → tracking and calibration → kinematic estimates → candidate event segmentation → candidate notation / Movement IR → practitioner review and correction`

Each stage needs:
- explicit capture purpose and consent;
- camera/sensor calibration and coordinate frame;
- tracking confidence, occlusion and dropout reporting;
- separation of raw media, estimated skeleton and semantic annotation;
- reviewable event boundaries and editable candidate scores;
- deletion and retention controls;
- no identity recognition or hidden profiling.

Start with manual scores, synthetic examples, props and room markers. Introduce body tracking only when a specific research question cannot be answered with less invasive means.

## 9. Cultural, methodological and ethical protocol

GENJE's work must be plural and practitioner-led. No imported notation or benchmark is a universal account of African movement.

For Turkana, Ateker, Genge or other situated research:
- identify the actual practitioners, community and context before defining categories;
- ask what should be documented and what should remain unrecorded;
- retain language, local terminology, attribution and disagreement;
- allow practitioners to correct transcription, segmentation and contextual description;
- distinguish individual testimony from community consensus;
- document access restrictions, consent, compensation and benefit-sharing where applicable;
- do not publish restricted ceremonial, personal or community material;
- preserve audio/video only under clear permissions and retention rules;
- never infer identity, health, emotion, personality, intention or capability from movement.

A multi-modal record may combine practitioner account, embodied demonstration, audio, video/stills, notation, variation register, contextual annotation and community review. The bundle is selected with practitioners; no medium is mandatory.

## 10. LMA reliability and evaluation caution

A 2019 *PLOS ONE* study, **“Assessing the reliability of the Laban Movement Analysis system,”** reported inter-rater Krippendorff's alpha values of approximately Space .66, Phrasing .66, Effort .46 and Shape .50 for its controlled study. This is a useful warning: more interpretive categories can show weaker agreement even among trained analysts. The study's controlled pantomime tasks and sample do not establish reliability across all dance forms or communities.

- [PLOS ONE study](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0218179)
- [NYU Movement Research Group — LMA](https://movementresearch.org/)
- [Laban/Bartenieff Institute of Movement Studies](https://labaninstitute.org/)
- [International Council of Kinetography Laban](https://ickl.org/)
- [Dance Notation Bureau](https://dancenotation.org/)

Evaluation must separate:
- syntactic validity and round-trip fidelity;
- timing and spatial reconstruction error;
- annotation agreement and disagreement;
- musical alignment;
- performer usability and correction effort;
- cultural/contextual validity as determined through an appropriate process;
- privacy, consent and rights compliance.

No single metric can stand in for all of these.

## 11. Staged research roadmap

| Stage | Work | Exit evidence |
|---|---|---|
| M0 — Evidence register | Verify primary sources, rights, dataset terms and model code status | Source ledger with claim/evidence labels |
| M1 — Movement IR v0 | Define event, phrase, body, time, space, relation and provenance records | Human-authored sample scores and schema tests |
| M2 — Notation adapters | Compare Labanotation, Motif and selected LMA annotation workflows | Worked examples and explicit loss reports |
| M3 — Music alignment | Link authored scores to audio, tempo maps and phrase structure | Timing tests with deliberate off-beat and polyrhythmic cases |
| M4 — Practitioner protocol | Co-design documentation and correction with actual practitioners | Consent, access and review protocol; no assumed community endorsement |
| M5 — Rendering | Inspect scores and paths in Blender or simpler native tools | Reproducible offline visualisation |
| M6 — Model interoperability | Evaluate LaMoGen/LLaMo/LAMP/diffusion adapters against fixed tasks | Reproducible comparison, rights audit and human evaluation |
| M7 — Observation | Evaluate manual annotation before optional MoCap/pose estimation | Calibration, uncertainty, deletion and correction tests |
| M8 — XR / live interaction | Only if a demonstrated creative need remains | Latency, participant control and failure-mode evidence |

### Acceptance criteria

- Scores can be authored and revised without AI.
- The representation distinguishes author instruction, observation, measurement and interpretation.
- Time, space and musical structure are not silently collapsed.
- Transformations report omissions, uncertainty and loss.
- Performer corrections and authorship remain attached to the record.
- Cultural terms are not generalised beyond their documented context.
- No inference or scoring of people is introduced.
- Dataset, model, media and performance rights are documented.
- Offline reproducibility is tested where feasible.
- A prototype is not called a product or a validated system without corresponding evidence.

## 12. Evidence and source register

### Primary research and project sources
- Jiang et al., [LaMoGen (arXiv:2603.11605)](https://arxiv.org/abs/2603.11605), CVPR 2026.
- [LaMoGen source repository](https://github.com/jjkislele/LaMoGen).
- [LaMoGen CVPR supplementary material](https://openaccess.thecvf.com/content/CVPR2026/supplemental/Jiang_LaMoGen_Language_to_CVPR_2026_supplemental.pdf).
- [AIST++ dataset documentation and terms](https://google.github.io/aistplusplus_dataset/).
- [FineDance, ICCV 2023](https://li-ronghui.github.io/finedance).
- [FACT, ICCV 2021](https://openaccess.thecvf.com/content/ICCV2021/html/Chen_เน).
- [ChoreDiffusion: Beat-Aware Diffusion for Music-to-Dance Generation (2026)](https://doi.org/10.3390/info17080808).
- [Labanotation generation from motion capture — IEEE Access search record](https://ieeexplore.ieee.org/search/searchresult.jsp?queryText=Labanotation%20Generation%20Based%20on%20Rhythm).
- [End-to-end Labanotation generation — IEEE ICME search record](https://ieeexplore.ieee.org/search/searchresult.jsp?queryText=end-to-end%20Labanotation%20generation).
- [Labanotation / Kinetography Laban institutional resources](https://ickl.org/).
- [LMA reliability study, PLOS ONE (2019)](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0218179).

### African movement documentation leads requiring further verification
- Latipher Amma Osei (2020), *Documenting Ghanaian dances through Labanotation*, *African Research Review* 14(2), 112–120. [University of Education, Winneba record](https://www.uew.edu.gh/theatre-arts/staff/laosei/publications/29001/detail).
- Felix Akinsipe (2015), *Development of 'Stick Figure' Notation for African Dances* — retain as a research lead; obtain and review the full text before making detailed claims.
- Grim-Feinberg and Wong Santos, *Movement Notation and the Analysis of Embodied Knowledge: Three Ethnographic Examples*. [Journal article](https://jashm.press.uillinois.edu/22.2/grim-feinberg.html).

These leads are not a complete survey of African movement research. The present research pass does not establish that no other African-led systems or archives exist. Search with regional practitioners, institutions, languages and specialist bibliographies before making any absence claim.

## 13. Relationship to existing GENJE and ecosystem records

This specification consolidates and extends, rather than replaces:
- [Labanotation, Movement Scores and Choreohacking](LABANOTATION-MOVEMENT-SCORE-RESEARCH-2026-11.md).
- [Kinetics, Livecoding & Reflective Interaction](KINETICS-LIVECODING-AND-IKAI-INTERACTION-2026-11-18.md).
- [Embodied Spatial Interaction Research](EMBODIED-SPATIAL-INTERACTION-RESEARCH-2026-11-14.md).
- [GENJE creative practice and provenance](creative-practice-and-provenance.md).

Related ecosystem boundaries:
- [FELOH Corpus](https://github.com/donfelohke/feloh-corpus) owns shared research evidence, source provenance and cross-domain indexing.
- [IKAI](https://github.com/donfelohke/Ikai) may support participant-directed reflection on records; it must not authoritatively interpret or score a performer.
- [WARENA](https://github.com/donfelohke/WARENA) owns infrastructure and reproducibility; no model or runtime is selected by this research note.

**Final position:** GENJE owns the creative and embodied questions. The Movement IR is a proposed bridge among human-authored scores, music, observation and execution—not a universal movement language, surveillance schema or automated judge.

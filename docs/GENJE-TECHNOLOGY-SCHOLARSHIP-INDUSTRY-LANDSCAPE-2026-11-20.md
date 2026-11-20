# GENJE — Technology, Scholarly & Industry Landscape

**Date:** 2026-11-20  
**Status:** RESEARCH / LANDSCAPE ASSESSMENT  
**Owner:** GENJE — movement, choreography, sound, performance and embodied creative practice  
**Related domains:** FELOH Corpus — shared evidence and provenance; IKAI — participant-directed reflection; WARENA — infrastructure and reproducibility  
**Implementation status:** Research only. No capture pipeline, dataset, choreography engine, model deployment, commercial service or partnership is claimed as implemented or approved.

## 1. Executive assessment

GENJE's opportunity is not to recreate a motion-capture studio, notation system, animation package, music sequencer or generic AI dance generator. Those already exist.

The opportunity is to integrate established tools and knowledge systems into a culturally situated, practitioner-controlled environment for documenting, composing, analysing, revisiting and performing movement in relation to sound, space, time and other performers.

The landscape establishes five findings:

1. **The technical ecosystem is mature in separate layers.** Optical and inertial motion capture, markerless pose estimation, 3D animation, music sequencing, notation and motion-generation research are available. They do not form a single culturally complete choreography system.
2. **African-centred computational dance research is active.** ATUNDA is a significant discovery: its repository describes 964 sequences covering 49 African and African Diaspora dance moves. GENJE must engage with existing work rather than claim this field is empty.
3. **Practitioner involvement changes model design and evaluation.** A 2026 CHI study with Voguing and Dancehall practitioners found that physical realism alone did not make generated movement useful; stylistic legibility and creative provocation mattered.
4. **Data and model licences are a major constraint.** Several leading research datasets and capture services are non-commercial or have separate media, performer and service terms. Open-source code does not automatically clear data, models, recordings or music.
5. **Kenya's creative-sector constraints are practical, not merely technical.** Research points to financing, equipment, skills, fair compensation and access barriers. A technically ambitious system that ignores these conditions will not be useful to most practitioners.

**Strategic position:** GENJE should be an integrative movement, music and embodied-knowledge research environment. Its distinctive contribution should be human authorship, African-centred context, interoperability, provenance and creative practice—not an attempt to replace upstream infrastructure.

## 2. Scope and research method

This landscape combines:
- scholarly literature and conference proceedings;
- primary project documentation and dataset repositories;
- software licences and terms of use;
- official vendor product and pricing pages;
- Kenyan policy and legislation;
- Kenyan creative-sector research and economic statistics;
- existing GENJE repository specifications and practice records.

Evidence labels:
- **PRIMARY:** paper, official repository, licence, standard or legislation.
- **INDUSTRY:** vendor-published product, feature or pricing information.
- **SECONDARY:** scholarly synthesis, industry report or archive description.
- **RESEARCH LEAD:** useful discovery requiring full-text, rights or community verification.
- **UNVERIFIED:** not tested or independently confirmed.

This is not a systematic review with exhaustive database searches, nor a procurement exercise. Prices and vendor terms are snapshots as of 2026-11-20. Legal analysis is a technical research aid, not legal advice.

## 3. Scholarly landscape

### 3.1 Computational dance and movement generation

The 2026 review *Music-driven dance generation: A comprehensive review* surveys music-driven dance-generation research through technological evolution, algorithms, objectives and system frameworks. It confirms that this is an established research field, not a greenfield problem. It is useful as a literature map; individual systems still need direct evaluation for GENJE's tasks.

Relevant research families include:

| Research / system | Main contribution | What GENJE should learn | What it does not establish |
|---|---|---|---|
| FACT / AI Choreographer (ICCV 2021) | Music-conditioned 3D dance generation using AIST++ | Music-motion conditioning and benchmark practice | Cultural validity or choreographic authorship |
| Bailando | Music-conditioned dance synthesis with structured motion representations | Music-to-motion architecture and temporal composition | A universal dance language |
| EDGE | Music-conditioned dance generation | Motion generation and beat-aware evaluation | Groove, social meaning or community acceptance |
| FineDance (ICCV 2023) | Fine-grained full-body dance dataset and generation | Detailed body movement and genre-conditioned research | African movement representation or commercial data rights |
| LaMoGen (CVPR 2026) | LLM-guided symbolic LabanLite composition for text-to-motion | Symbolic intermediate representation as an adapter concept | Full Labanotation, full LMA or human-authored choreography |
| LLaMo (CVPR 2026) | Unified motion understanding and generation using continuous motion tokens | Continuous representations and unified modelling | Interpretability or cultural legitimacy |
| LAMP (CVPR 2026) | LLM-guided motion planning through a structured DSL | Explicit motion-program and constraint design | Dance-specific choreography; its focus is controllable video motion planning |
| DanceLDM (2026) | Latent diffusion for music/text-conditioned dance generation and editing | Conditional generation and editing | Practitioner acceptance or rights clearance |
| ChoreDiffusion (2026) | Beat-aware diffusion for music-to-dance | Beat-conditioned generation | Complete musicality or choreographic intent |
| Motion-to-Labanotation studies | Convert tracked movement into candidate notation using segmentation and sequence models | Reverse-direction conversion and review workflows | Authoritative notation without human validation |

The published systems are not a controlled head-to-head benchmark. Results from different datasets, skeletons, preprocessing, hardware and evaluation protocols must not be compared as if they came from one experiment.

Core sources:
- Music-driven dance generation review (2026): https://doi.org/10.1016/j.neucom.2026.133466
- FACT / AI Choreographer: https://openaccess.thecvf.com/content/ICCV2021/html/Li_AI_Choreographer_Music_Conditioned_3D_Dance_Generation_With_AIST_ICCV_2021_paper.html
- AIST++: https://google.github.io/aistplusplus_dataset/
- FineDance: https://openaccess.thecvf.com/content/ICCV2023/html/Li_FineDance_A_Fine-grained_Choreography_Dataset_for_3D_Full_Body_Dance_Generation_ICCV_2023_paper.html
- LaMoGen: https://arxiv.org/abs/2603.11605
- LLaMo: https://openaccess.thecvf.com/content/CVPR2026/html/Li_LLaMo_Scaling_Pretrained_Language_Models_for_Unified_Motion_Understanding_and_CVPR_2026_paper.html
- LAMP: https://openaccess.thecvf.com/content/CVPR2026/html/Kizil_LAMP_Language-Assisted_Motion_Planning_for_Controllable_Video_Generation_CVPR_2026_paper.html
- DanceLDM: https://doi.org/10.1007/s00530-026-02311-z
- ChoreDiffusion: https://doi.org/10.3390/info17080808

### 3.2 Practitioner-centred movement generation: CHI 2026

**Pank, Carrascosa, Onikeku, Frusco, Craig and Barmpoutis, “Real-Time Computer-Assisted Afrogenic Dance Move Recognition and Analysis,” ACM IMX 2026, pp. 316–327. DOI: 10.1145/3788851.3805020.**

This is a significant African-centred computational dance contribution. The associated ATUNDA project describes 964 sequences and 49 distinct African and African Diaspora dance moves. Its pipeline uses video-derived pose representations, including MediaPipe, FMPose3D and SAMbody4D. The paper proposes learned movement classification and similarity analysis for interactive analysis, visualisation and Unity reuse.

Critical interpretation:
- A classifier's confusion matrix can reveal patterns of similarity under that model and dataset; it does not prove authorship, ownership, plagiarism or cultural equivalence.
- The dataset's coverage must be assessed from its actual move inventory, source communities, performers, capture conditions, consent and documentation—not inferred from the term “Afrogenic”.
- The repository reports phase 3 as in progress. The 964/49 figures describe the published repository snapshot, not a permanently complete or representative catalogue.
- The dataset's custom licence prohibits commercial use, expires one year after download and requires deletion on expiry. The project notes that performers may request removal or contribute new data.
- The paper is labelled CC BY-NC-ND 4.0 in its surfaced publication record; the dataset is under a separate Atunda licence. Do not conflate these licences.

Sources:
- Repository and dataset statement: https://github.com/digitalworlds/atunda
- IMX 2026 paper: https://doi.org/10.1145/3788851.3805020
- Author research record: https://angelosbarmpoutis.com/

**GENJE implication:** ATUNDA should be treated as an existing research neighbour and possible collaboration lead. GENJE should compare methods and governance, cite the work and approach its researchers before proposing overlapping dataset or classification work.

A separate 2026 CHI paper, “Designing Movement Generation Models in Collaboration With Voguing And Dancehall Dancers” (Article 291; DOI: 10.1145/3772318.3791515), reports a three-year collaboration with two dancers from a Paris-based collective. Dancers curated repertoire, participated in motion capture and assessed successive generation models. The study found that physically realistic but stylistically illegible movements were less compelling than outputs that were either faithful to the repertoire or sufficiently unfamiliar to provoke creative reinterpretation. Its Korai interface helped researchers and dancers inspect source and generated motion.

This study is a method reference, not a universal conclusion: two practitioners in one collective cannot represent all dancers or traditions. Its important lesson is methodological: practitioners must influence the dataset, representation, interface and evaluation—not merely review a finished model.

Source: https://doi.org/10.1145/3772318.3791515

### 3.3 African and East African scholarship

**Kenya — Agata and Kirui, “The Evolution of Digital Dance: Choreography in the Age of Motion Capture and Avatars, a case of Nairobi City County.”** *Journal of Visual and Performing Arts*, 3(1), 44–52; DOI: 10.58721/jvpa.v3i1.1515. Published online 20 January 2026. The study uses netnography around Matata, the Heroes of Kenya avatar project and Nairobi motion-capture studios. It discusses social-media choreography, digital heritage, ownership and cultural transmission. This is a useful Nairobi entry point, not a national census or a full survey of Kenyan movement traditions.

Source: https://doi.org/10.58721/jvpa.v3i1.1515

**Ghana — Latipher Amma Osei (2020), “Documenting Ghanaian dances through Labanotation.”** *African Research Review* 14(2), 112–120; DOI: 10.4314/afrrev.v14i2.11. The article examines Labanotation as one possible documentation approach, identifies challenges in its application to African dance and discusses combining notation with cinematography.

Source: https://www.uew.edu.gh/theatre-arts/staff/laosei/publications/29001/detail

**Northern Uganda — Ronald Kibirige (2015), “Notation of an African Indigenous Dance: An Inquiry on the Application of Labanotation Theory to Understand Myel Bwola from the Acholi Sub-Region of Northern Uganda.”** Proceedings of the 29th International Council of Kinetography Laban conference. This is a valuable East African precedent for studying a specific dance idiom through notation, while recognising the tension between formal transcription and embodied/oral knowledge.

Source: https://ickl.org/wp-content/uploads/2017/07/Proceedings_ICKL_2015_web.pdf

**Ghanaian historical documentation — Odette Blum, African Dances and Games.** The Dance Notation Bureau describes a body of work combining movement notation with dance descriptions, cultural/historical background and rhythm, based on work in Ghana in 1966–1968. The archive warns that reproduction is restricted; do not copy its scores, images or publication without permission.

Source: https://www.dancenotation.org/theory-bulletin-board/african-dances-and-games/

**Research conclusion:** African dance documentation is not absent. It is distributed across scholarship, archives, practitioner networks, film, music, notation and emerging computational datasets. The evidence does not justify claiming that GENJE is the first or only African movement research initiative. The more defensible gap is a lack of sufficiently connected, interoperable, locally governed and practitioner-directed resources for particular movement communities and creative workflows.

### 3.4 Movement-analysis reliability and notation discipline

Labanotation/Kinetography Laban, Motif, Laban Movement Analysis (LMA) and Bartenieff Fundamentals are related but not interchangeable.

A 2019 reliability study of LMA reported Krippendorff's alpha values of approximately:
- Space: 0.66
- Phrasing: 0.66
- Effort: 0.46
- Shape: 0.50

These results are specific to the study's stimuli, raters and procedure; they do not invalidate LMA. They do demonstrate why qualitative annotations should preserve the observer, training, vocabulary, context and disagreement rather than being treated as objective sensor labels.

Source: https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0218179

**Design implication:** retain multiple attributed interpretations. Do not force consensus, reduce qualitative Effort or Shape to unqualified numeric scores, or claim that machine classification is equivalent to trained movement analysis.

## 4. Existing technology landscape

### 4.1 Capture approaches

| Approach | Strengths | Limitations | Suitable research role |
|---|---|---|---|
| Manual score / practitioner annotation | Lowest equipment dependency; authorship and context can be explicit | Labour-intensive; depends on expertise and documentation method | First-line GENJE method |
| Video recording | Accessible, replayable, retains performance context | Occlusion, camera perspective, rights, privacy, limited 3D recovery | Contextual evidence and review |
| Marker-based optical capture | High-quality 3D trajectories and multi-performer capture in controlled volume | Camera infrastructure, markers, calibration, specialist operators and cost | High-fidelity research or studio partnership |
| Inertial suit / IMU | Portable, less dependent on camera line-of-sight, suitable for mobile capture | Drift, calibration, magnetic/environmental issues, suit and software dependence | Mobile performance capture comparison |
| Markerless pose estimation | Lower entry barrier; can use ordinary video | Occlusion, viewpoint, lighting, body diversity, clothing and fast motion can degrade estimates | Candidate observation adapter, never ground truth |
| Smartphone-based biomechanics | Low hardware barrier for specific validated tasks | Service terms, model/task scope and privacy conditions; not a dance-specific validated system | Research comparator only |

**Capture decision:** start with score-first and practitioner-led methods. Do not purchase optical or inertial capture hardware before a task-specific validation study demonstrates that manual notation, ordinary video and borrowed studio access are insufficient.

### 4.2 Markerless and open-source software

| Candidate | Function | Licence / service qualification | GENJE assessment |
|---|---|---|---|
| MMPose | Pose-estimation toolkit: multi-person body, hand, face and whole-body tasks | Apache 2.0 repository licence | Strong candidate for isolated technical experiments; Python/PyTorch stack |
| DeepLabCut | User-defined markerless keypoint tracking, including human research | LGPL-3.0 | Useful when custom landmarks and domain-specific labelling matter |
| OpenPose | Multi-person body, face, hand and foot keypoints | Non-commercial research licence; commercial licence required | Not a default for any commercial pipeline |
| OpenCap | Smartphone video-based movement dynamics | Core source repositories Apache 2.0; hosted service terms restrict commercial-entity use and describe developer access to submitted videos | Separate code from service terms; do not assume hosted service is local-first or commercially usable |
| Blender | 3D animation, rigging, visual inspection and motion interchange | GPL software | Preferred visual inspection candidate; existing BVH import/export |
| LaMoGen | Symbolic text-to-motion research | MIT repository does not clear datasets, model weights, SMPL assets or dependencies | Isolated research adapter only |

Sources:
- MMPose: https://github.com/open-mmlab/mmpose
- DeepLabCut: https://github.com/DeepLabCut/DeepLabCut
- OpenPose: https://github.com/CMU-Perceptual-Computing-Lab/openpose
- OpenCap code: https://github.com/stanfordnmbl/opencap-core
- OpenCap service terms: https://www.opencap.ai/terms-conditions
- OpenCap study: https://doi.org/10.1371/journal.pcbi.1011462
- Blender BVH manual: https://docs.blender.org/manual/en/latest/files/import_export/bvh.html
- LaMoGen: https://github.com/jjkislele/LaMoGen

Important OpenCap distinction: its source-code repositories are published under Apache 2.0, but the hosted service terms state that it is provided for non-commercial academic/non-profit research and education, and that submitted videos are visible to the development team and may be used for algorithm development. Code licensing and hosted-service terms are different legal objects.

### 4.3 Commercial motion-capture systems

| Vendor / platform | Capture model | Published capabilities | Commercial qualification |
|---|---|---|---|
| Vicon Shōgun | Optical and markerless | Live, markerless and post-production capture; finger detail, retargeting and streaming | Professional studio product; pricing generally sales-led |
| OptiTrack Motive | Optical marker-based | Human skeletons, rigid bodies, live and post capture | Published software prices; camera hardware and full system cost additional |
| Xsens MVN | Inertial suit | Multi-actor options, live streaming, local export and FBX/BVH/C3D/MVNX formats | Subscription licensing; hardware and software costs |
| Rokoko Studio / Vision | Inertial and video-AI options | Recording, cleanup, export, retargeting, live streaming and cloud workflows | Tiered subscription; local storage/no cloud sync listed for Enterprise |

**Price snapshot — vendor-published USD, 20 November 2026:**

- OptiTrack Motive:Body: USD 4,999 perpetual software licence with one year of updates; subsequent annual maintenance listed at USD 2,499.
- Motive:Body Unlimited: USD 9,999; subsequent annual maintenance USD 4,999.
- Rokoko annual billing: Basic USD 10/month, Plus USD 20/month, Pro USD 50/month; Enterprise starts at USD 100/month. Monthly billing lists USD 12, 28, 70 and 150 respectively.
- Rokoko Enterprise advertises local storage and no cloud synchronisation. Lower tiers include cloud storage and limited offline periods.
- Xsens publishes subscription durations and feature tiers, but the cited page does not provide a complete public price list.
- Vicon Shōgun product information is public, but a comparable complete price is not published on the cited product page.

Sources:
- OptiTrack Motive pricing: https://www.optitrack.com/software/motive/pricing
- Rokoko plans: https://www.rokoko.com/pricing
- Xsens Animate: https://www.xsens.com/motion-capture/xsens-mvn-animate
- Vicon Shōgun: https://www.vicon.com/software/shogun/

These figures are software subscription/licence prices, not total system costs. They exclude cameras, suits, sensors, markers, computers, room treatment, shipping, taxes, import duties, training, service contracts and operator time. They are not a procurement recommendation.

### 4.4 Interchange formats and event protocols

Reuse existing formats for the data they were designed to carry:

| Format / protocol | Established role | GENJE boundary |
|---|---|---|
| BVH | Skeleton hierarchy and joint animation | Use for basic skeleton interchange; retain coordinate and frame-rate metadata |
| FBX | 3D scene and character-animation interchange | Useful for animation pipelines; vendor/ecosystem dependence and versioning need review |
| C3D | Motion-capture point and analogue data | Useful for capture/research interchange; not a choreographic semantic language |
| SMPL / SMPL-X | Parametric body-model representations | Model/body representation, not cultural movement notation |
| OSC | Network messages for real-time control and event communication | Strong candidate for movement/audio/visual bridges |
| MIDI 1.0 / 2.0 | Musical performance and device-control messages | Use for musical events and controller semantics, not as a full movement database |
| SQLite | Local relational data store | Appropriate for local records and provenance |
| Git | Version history and collaborative source control | Appropriate for score/code revisions, not large raw media storage by itself |

Blender's BVH importer explicitly exposes scale, rotation order, forward/up axes and frame-rate handling. These are not cosmetic details: a wrong coordinate or clock transform can invert or distort movement.

TidalCycles sends patterned OSC messages and can control other synths through OSC or MIDI. It is embedded in Haskell and uses a cycle-based pattern language. This makes it a useful existing livecoding system; it need not become GENJE's canonical semantic layer.

Sources:
- Blender BVH: https://docs.blender.org/manual/en/latest/files/import_export/bvh.html
- TidalCycles: https://tidalcycles.org/docs/
- Tidal OSC: https://tidalcycles.org/docs/configuration/MIDIOSC/osc/
- MIDI 2.0 / UMP: https://midi.org/universal-midi-packet-ump-and-midi-2-0-protocol-specification

## 5. Dataset and rights assessment

**Availability is not permission. A repository's code licence does not automatically license its data, performer recordings, music, assets or model weights.**

| Dataset / archive | Research value | Rights / access issue | Decision |
|---|---|---|---|
| ATUNDA | African and Diaspora movement; 964 sequences, 49 moves | Custom one-year licence, non-commercial use only, deletion on expiry; performer withdrawal is acknowledged | Priority comparison and collaboration lead; no commercial training |
| AIST++ | 1,408 sequences, ten genres, multi-view 3D keypoints and paired music | Annotations CC BY 4.0; source AIST Dance DB videos/music academic research only absent written commercial permission | Benchmark carefully; separate annotation rights from source media rights |
| FineDance | Fine-grained full-body dance | Non-commercial scientific research licence for data and software | Research comparator only |
| AMASS | Broad motion-capture archive and body-model data | Non-commercial scientific research, education or artistic use; commercial use prohibited without permission | Research only absent separate licence |
| HumanML3D | Text-to-motion dataset derived from existing motion collections | Repository MIT licence does not establish unrestricted rights to every underlying source | Verify lineage and upstream terms |
| Cyprus DanceDB | Traditional dance archive with video, C3D, FBX and BVH | University-controlled non-commercial research terms | Archival design reference; obtain permissions before reuse |

Primary sources:
- ATUNDA: https://github.com/digitalworlds/atunda
- AIST++ annotations: https://google.github.io/aistplusplus_dataset/
- AIST Dance DB terms: https://aistdancedb.ongaaccel.jp/terms_of_use/
- FineDance licence: https://github.com/li-ronghui/FineDance/blob/main/LICENSE
- AMASS licence: https://amass.is.tue.mpg.de/license.html
- HumanML3D repository: https://github.com/EricGuo5513/HumanML3D
- Cyprus DanceDB: https://dancedb.cs.ucy.ac.cy/

### 5.1 Consequences for GENJE

1. Maintain a dataset register with source, custodian, version, licence, performer consent, media rights, allowed purposes, expiry, withdrawal process and redistribution conditions.
2. Keep research-only data separate from any commercial assets or training workflow.
3. Never train on public social-media dance videos merely because they can be downloaded.
4. Preserve performer and choreographer attribution; do not treat a similarity score as proof of ownership or infringement.
5. Design deletion and withdrawal propagation before capture, not as a later feature.
6. Prefer original, explicitly consented, purpose-limited research material for any future GENJE-specific work, subject to community protocols and law.

## 6. Kenyan industry and market context

### 6.1 Creative-sector economics

FSD Kenya's 2021 creative-sector research estimated 275,375 creative enterprises, of which 44,614 were registered, and identified financing, market access and weak institutional support as important constraints. These are study estimates, not a current official census.

Source: https://www.fsdkenya.org/research-and-publications/report-new-business-models-for-financing-the-creative-sector-research/

Genesis Analytics' November 2024 *Creative Sector and Youth Employment – Kenya* report is more directly useful for technology adoption. It identifies access to financing and equipment as key constraints; its survey's technology-access responses identify finance (44%) and equipment (33%) as the leading challenges. It notes 64 film/motion-capture enterprises listed on KFTV in 2021, adjusted to 68 in its 2024 sizing exercise. This is not a count of specialist motion-capture studios: it is a directory-based film/motion-capture enterprise estimate.

The report also highlights the importance of smartphones and social media, while describing the cost and skills barriers around more advanced tools.

Source: https://fundforyouthemployment.nl/wp-content/uploads/2024/12/Learning-agenda-research-study-on-Kenyas-creative-ecosystem_v3final.pdf

Asena, Njuguna and Nyakinya's 2026 open-access study, *Empowering young art entrepreneurs: lowering barriers for decent work in Kenya's creative industry*, draws on 29 stakeholder interviews and ten focus groups involving 80 art entrepreneurs aged 18–35. It reports that digital migration and open platforms create opportunities, but pay inequality, limited social protection, high production costs, inadequate training and regulatory barriers remain significant constraints.

Source: https://doi.org/10.1007/s40497-025-00478-9

The Kenya National Bureau of Statistics' 2023 Film Industry Satellite Account estimated for 2022:
- gross output: KSh 86.9 billion;
- gross value added: KSh 38.1 billion;
- jobs supported: 42,823;
- earnings across the defined activities: KSh 14.5 billion.

These are broad film and broadcasting sector figures, not dance, motion-capture or GENJE market size.

Source: https://kenyafilmcommission.go.ke/wp-content/uploads/2023/11/Film-Industry-Satelite-Account-FISA-Report.pdf

### 6.2 Industry segments relevant to GENJE

| Segment | Buyers / participants | Existing infrastructure | Potential value of GENJE research |
|---|---|---|---|
| Independent dancers and choreographers | Individual artists, collectives, teachers | Phone video, studios, social platforms, notation and editing tools | Score authoring, repertoire documentation, music-linked rehearsal and provenance |
| Music and live performance | Musicians, producers, venues, festivals | DAWs, livecoding, MIDI/OSC, lighting and projection systems | Movement-responsive sound and audiovisual composition |
| Film, animation and games | Production houses, animators, game studios | Optical/IMU capture, retargeting, Blender and commercial animation tools | Culturally grounded performance references and licensed movement assets |
| Education and research | Universities, dance schools, cultural institutions | Archives, studios, cameras, notation and motion-analysis software | Teaching records, multi-modal archives and comparative research |
| Museums and cultural heritage | Community custodians, museums, archives | Oral history, film, metadata catalogues and digital exhibits | Community-governed records and linked movement/music/context documentation |
| Interactive installations and XR | Artists, galleries, event producers | OpenXR, tracking, spatial displays and real-time graphics | Authored movement interaction and participant-controlled spatial performance |

### 6.3 Industry opportunity assessment

The strongest near-term opportunity is not to sell an expensive capture platform. It is to build competence and partnerships around existing systems and unmet creative workflows:

- movement documentation and digital archiving with practitioners;
- choreographic and livecoding workshops;
- production support for movement-driven audiovisual performances;
- licensed and attributed animation/motion references;
- education and research collaborations;
- interactive installation and XR performance experiments.

Any commercial opportunity must be assessed separately from research rights. A non-commercial academic dataset cannot silently become a commercial asset.

### 6.4 Market sizing discipline

There is no defensible current market-size figure in the sources reviewed for an African dance-specific motion-capture or choreographic-computing market. Do not convert Kenya's overall film-sector output or creative-enterprise estimates into a GENJE addressable market.

A future bottom-up estimate should separately count:
- target institutions and studios by country;
- independent choreographers, collectives and educators;
- relevant annual production, training and archive budgets;
- capture/animation service spend;
- software and hardware procurement;
- willingness to pay for documentation, workshops and licensed assets;
- procurement cycles and grant-funded research activity.

Until that evidence exists, market opportunity is qualitative, not a TAM/SAM/SOM claim.

## 7. Governance and legal considerations in Kenya

This is a research-level risk assessment, not legal advice.

### 7.1 Data Protection Act

Kenya's Data Protection Act, 2019 defines biometric data as personal data resulting from specific technical processing based on physical, physiological or behavioural characterisation. It includes biometric data within sensitive personal data. A movement-capture dataset may contain personal data; whether a particular representation qualifies as biometric data depends on its processing and use, not merely the fact that it contains body coordinates.

The Act's principles include lawful, fair and transparent processing; specified legitimate purposes; data minimisation; accuracy; limited retention; and conditions for cross-border transfer. Data subjects have rights to information, access, objection and correction. A data protection impact assessment is required before processing likely to create high risk.

Sources:
- https://new.kenyalaw.org/akn/ke/act/2019/24/eng%402019-11-15/source
- https://www.odpc.go.ke/

### 7.2 Traditional Knowledge and Cultural Expressions Act

Kenya's Protection of Traditional Knowledge and Cultural Expressions Act, 2016 is directly relevant where a project documents, adapts, publishes or commercially exploits protected traditional knowledge or cultural expressions.

The Act recognises community custodianship and collective ownership; provides for prior informed consent and community rules; requires acknowledgement and respect for cultural values; and provides for fair and equitable benefit sharing for commercial or industrial use. Its provisions also address derivative works, licensing and community consultation.

Sources:
- https://new.kenyalaw.org/akn/ke/act/2016/33/eng%402022-12-31/source
- https://www.wipo.int/wipolex/en/legislation/details/21462

### 7.3 Required governance controls

Before any future recording or publication:
- identify individual performers, choreographers, community holders and other rights holders;
- explain purpose, recording methods, access, storage, publication and potential reuse;
- distinguish individual consent from community-level authorisation where protected cultural expressions are involved;
- document customary protocols and community decision-making;
- agree on attribution, access tiers, retention, withdrawal and deletion;
- document benefit sharing before commercial or industrial exploitation;
- do not assume public performance, online posting or social-media availability means unrestricted permission;
- do not imply a community endorses a model or archive without documented authority.

## 8. GENJE architecture implications

The existing GENJE Movement IR document remains the proposed semantic/interoperability contract. It should not be inflated into a replacement for established notation, skeleton formats, animation systems or music protocols.

### 8.1 Reuse / integrate / adapt / invent register

| Layer | Existing foundation | Decision | Why |
|---|---|---|---|
| Detailed notation | Labanotation / Kinetography Laban | REUSE | Established notation tradition; require qualified human authorship |
| Selective movement ideas | Motif | REUSE | Appropriate where full notation is unnecessary |
| Qualitative movement analysis | LMA / Bartenieff | REUSE / ADAPT | Use with attribution, training and observer context |
| Skeleton animation | BVH / FBX / C3D | REUSE | Existing interchange formats |
| Body models | SMPL-family | ADAPT | Useful for model interoperability; not cultural semantics |
| Pose estimation | MMPose / DeepLabCut and other tools | ISOLATED ADAPTER | Mature upstream work; verify licences and task accuracy |
| 3D inspection | Blender | REUSE | Existing animation and motion inspection |
| Live sound | SuperCollider / TidalCycles | REUSE / CONNECT | Existing synthesis and rhythmic pattern systems |
| Event transport | OSC / MIDI | REUSE | Established communication protocols |
| Local record store | SQLite | REUSE | Mature local database |
| Reproducible environment | GNU Guix | REUSE | WARENA infrastructure policy |
| Semantic integration | GENJE Movement IR | MINIMAL ADAPTIVE CONTRACT | Bridges authored score, notation, sound, observation and rendering |
| Cultural provenance and access | Existing legal/community protocols plus explicit metadata | ADAPT | Needs context-specific governance |
| New universal notation | None justified | DO NOT INVENT | No evidence of necessity; risks duplicating established systems |

### 8.2 WARENA-compatible research stack

Candidate stack, not selected implementation:
- Emacs / Org for authoring, annotation and research notebooks.
- Guile / Scheme for canonical data transformations and validation.
- SQLite for local structured records and metadata.
- GNU Guix for reproducible environments.
- Blender for visual inspection and animation interchange.
- SuperCollider and TidalCycles for sound and rhythmic performance.
- OSC and MIDI for event communication.
- Python-based MMPose or other upstream tools only as isolated compatibility adapters, if their use is justified and permitted.

Python may be used at a compatibility boundary for upstream research systems. It should not become the canonical WARENA runtime. JavaScript/browser frameworks are excluded from the WARENA application architecture under the existing technology policy.

### 8.3 Event/time architecture

Maintain independent but linkable streams:
1. authored movement score;
2. observed or measured movement;
3. music and rhythm;
4. visual or spatial presentation;
5. reflection and review.

Each stream needs its own clock and provenance. A shared event identifier may associate a movement cue with a musical event without claiming causation or semantic equivalence. Record offset, drift, frame rate, sampling rate and uncertainty.

## 9. Evaluation framework

Do not compress all quality into a single “dance realism” score.

| Evaluation dimension | Possible method | Who should assess |
|---|---|---|
| Notation fidelity | Compare score against trained human transcription and corrections | Qualified notation practitioners |
| Kinematic fidelity | Calibrated motion comparison with uncertainty | Motion-capture / biomechanics specialists |
| Temporal alignment | Beat/phrase timing analysis with clock error reporting | Musicians, choreographers and technical evaluators |
| Spatial fidelity | Coordinate, formation and pathway comparison | Choreographers and spatial researchers |
| Stylistic legibility | Situated practitioner interpretation | Practitioners of the relevant style |
| Creative usefulness | Rehearsal observation, interviews and reflective practice | Dancers and choreographers |
| Cultural validity | Community-led review and documented authority | Relevant holders and practitioners |
| Interoperability | Round-trip tests and transformation loss reports | Technical researchers |
| Reproducibility | Pinned environment, source, data rights and repeatable procedure | Independent technical reviewers |
| Governance | Consent, access, withdrawal and deletion tests | Participants, custodians and data stewards |

Required controls:
- distinguish authorship, observation, measurement, inference and interpretation;
- retain disagreements and alternative readings;
- do not infer emotion, identity, health, personality, intent or ability;
- do not rank performers or assess bodies against a normative ideal;
- treat generated motion as a proposal, not an authored cultural account;
- ensure practitioners can correct, reject or remove their contributions.

## 10. Risks and mitigations

| Risk | Consequence | Mitigation |
|---|---|---|
| Recreating existing tools | Waste and fragmented ecosystem | Inventory upstream systems before design |
| Dataset licence violation | Legal and reputational exposure | Dataset-level rights ledger and commercial/non-commercial separation |
| Cultural extraction | Loss of trust and misappropriation | Community authority, prior informed consent and benefit sharing |
| Model overclaim | Confusing realism with cultural validity | Multi-dimensional practitioner-led evaluation |
| Sensor error | False movement interpretation | Calibration, uncertainty and human review |
| Data exposure | Privacy and safety harm | Local-first, minimisation, access controls and deletion |
| Proprietary vendor lock-in | High switching costs and data dependency | Export tests and open interchange formats |
| High equipment cost | Low adoption and poor sustainability | Begin with manual scores, ordinary video and borrowed facilities |
| Weak local market evidence | Overinvestment | Bottom-up demand validation before procurement |
| AI displaces authorship | Reduced agency and cultural distortion | Human-authored source records and explicit approval boundaries |

## 11. Recommended research programme

| Stage | Work | Exit evidence |
|---|---|---|
| R0 — Existing-work audit | Verify papers, tools, licences, formats, repositories and existing GENJE work | Source register and reuse/adapt/invent decisions |
| R1 — African research network | Review ATUNDA, Kenyan, Ghanaian, Ugandan and other regional work; identify custodians and practitioners | Annotated regional literature and collaboration map |
| R2 — Task specification | Choose one real choreography or livecoding task and define what must be represented | Task-specific requirements, no premature platform design |
| R3 — Score-first workflow | Document a human-authored score and performance with agreed multimodal records | Reusable research record and practitioner corrections |
| R4 — Interoperability test | Import/export existing notation, BVH/FBX/C3D and timing references | Loss reports and round-trip evidence |
| R5 — Music interaction | Connect score events to sound through existing OSC/MIDI tools | Timing, latency and musical evaluation |
| R6 — Visual inspection | Reuse Blender or another suitable native tool | Repeatable inspection workflow |
| R7 — Capture comparison | Compare manual annotation, video-derived pose and borrowed professional capture | Accuracy, cost, privacy and usability evidence |
| R8 — Generative comparison | Evaluate existing models on fixed, rights-cleared tasks with practitioners | Multi-dimensional evaluation, not leaderboard-only claims |
| R9 — Situated practice | Conduct community-led research and governance review | Documented permissions, authority, corrections and benefit terms |
| R10 — XR/live interaction | Consider only after a specific creative need is demonstrated | Latency, accessibility, participant-control and failure evidence |

## 12. Strategic recommendations

### Immediate
1. Treat ATUNDA as a priority research neighbour; study its paper, dataset schema, move taxonomy and licence. Explore scholarly contact before planning overlapping work.
2. Correct any claim that no African computational dance dataset exists.
3. Build a rights-aware source register covering datasets, models, code, media, music and community contributions.
4. Use existing GENJE movement, notation, kinetics and provenance documents as one connected research base.
5. Continue score-first research before camera or wearable capture.

### Near term
6. Conduct a small practitioner-led documentation study using an existing notation approach and multi-modal evidence, with explicit permissions.
7. Test a minimal interoperability workflow using established formats rather than inventing a new motion format.
8. Evaluate OSC/MIDI links between TidalCycles/SuperCollider and authored movement events.
9. Establish a Kenya/East Africa research map, including dance practitioners, universities, archives, studios and cultural custodians.
10. Build a realistic cost model from borrowed/partner facilities before considering hardware purchases.

### Longer term
11. Compare markerless, inertial and optical capture only against a documented creative requirement.
12. Evaluate generative systems only on rights-cleared, practitioner-curated tasks.
13. Consider a GENJE-specific dataset only where community governance, consent, withdrawal, rights, resourcing and long-term stewardship are established.
14. Treat XR as an optional presentation and rehearsal environment, not a prerequisite or a new platform to build.

## 13. Source register

### Scholarly and technical
- Music-driven dance generation: A comprehensive review (2026): https://doi.org/10.1016/j.neucom.2026.133466
- CHI 2026 practitioner collaboration: https://doi.org/10.1145/3772318.3791515
- ATUNDA repository: https://github.com/digitalworlds/atunda
- ATUNDA IMX 2026 paper: https://doi.org/10.1145/3788851.3805020
- Kenya digital dance study: https://doi.org/10.58721/jvpa.v3i1.1515
- Osei, Ghanaian dance documentation: https://www.uew.edu.gh/theatre-arts/staff/laosei/publications/29001/detail
- Kibirige, Myel Bwola notation: https://ickl.org/wp-content/uploads/2017/07/Proceedings_ICKL_2015_web.pdf
- LMA reliability study: https://doi.org/10.1371/journal.pone.0218179
- AIST++: https://google.github.io/aistplusplus_dataset/
- FineDance: https://openaccess.thecvf.com/content/ICCV2023/html/Li_FineDance_A_Fine-grained_Choreography_Dataset_for_3D_Full_Body_Dance_Generation_ICCV_2023_paper.html
- AMASS: https://amass.is.tue.mpg.de/
- Cyprus DanceDB: https://dancedb.cs.ucy.ac.cy/

### Technology and industry
- MMPose: https://github.com/open-mmlab/mmpose
- DeepLabCut: https://github.com/DeepLabCut/DeepLabCut
- OpenPose: https://github.com/CMU-Perceptual-Computing-Lab/openpose
- OpenCap: https://www.opencap.ai/
- Blender BVH: https://docs.blender.org/manual/en/latest/files/import_export/bvh.html
- TidalCycles: https://tidalcycles.org/docs/
- OptiTrack Motive pricing: https://www.optitrack.com/software/motive/pricing
- Rokoko pricing: https://www.rokoko.com/pricing
- Xsens Animate: https://www.xsens.com/motion-capture/xsens-mvn-animate
- Vicon Shōgun: https://www.vicon.com/software/shogun/

### Kenya industry and governance
- FSD Kenya creative-sector research: https://www.fsdkenya.org/research-and-publications/report-new-business-models-for-financing-the-creative-sector-research/
- Genesis Analytics, Creative Sector and Youth Employment — Kenya (2024): https://fundforyouthemployment.nl/wp-content/uploads/2024/12/Learning-agenda-research-study-on-Kenyas-creative-ecosystem_v3final.pdf
- Asena et al. (2026), Kenya creative industry: https://doi.org/10.1007/s40497-025-00478-9
- KNBS Film Industry Satellite Account (2023): https://kenyafilmcommission.go.ke/wp-content/uploads/2023/11/Film-Industry-Satelite-Account-FISA-Report.pdf
- Kenya Data Protection Act: https://new.kenyalaw.org/akn/ke/act/2019/24/eng%402019-11-15/source
- Kenya Protection of Traditional Knowledge and Cultural Expressions Act: https://new.kenyalaw.org/akn/ke/act/2016/33/eng%402022-12-31/source

## 14. Relationship to existing GENJE documentation

This landscape complements, and does not replace:
- [GENJE Movement IR and Motion Research (2026-11-20)](GENJE-MOVEMENT-IR-AND-MOTION-RESEARCH-2026-11-20.md) — canonical movement semantics and adapter proposal.
- [Labanotation, Movement Scores and Choreohacking](LABANOTATION-MOVEMENT-SCORE-RESEARCH-2026-11.md) — notation and plural documentation.
- [Kinetics, Livecoding & Reflective Interaction](KINETICS-LIVECODING-AND-IKAI-INTERACTION-2026-11-18.md) — movement, sound and participant-directed reflection.
- [Embodied Spatial Interaction Research](EMBODIED-SPATIAL-INTERACTION-RESEARCH-2026-11-14.md) — spatial and XR boundaries.
- [GENJE Creative Practice and Provenance Standard](creative-practice-and-provenance.md) — authorship, rights and reproducibility.

Ownership remains:
- GENJE: movement, choreography, sound, livecoding, creative authorship and performance context.
- WARENA: infrastructure, system integration and reproducibility.
- IKAI: participant-directed reflection, consent and privacy.
- FELOH Corpus: shared evidence, provenance, governance and cross-project navigation.

**Final position:** reuse before adaptation; adaptation before invention; invention only where evidence establishes a genuine gap. GENJE should build relationships and interoperability around existing African and global work, preserve practitioner authority, and document what is actually tested. No product, engine, dataset, capture pipeline, partnership or deployment is claimed by this research assessment.

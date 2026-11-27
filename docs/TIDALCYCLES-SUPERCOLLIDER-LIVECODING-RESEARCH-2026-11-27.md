# GENJE — TidalCycles, SuperCollider and Live Audiovisual Research

**Date:** 27 November 2026  
**Owner:** GENJE / EXPRESSION  
**Status:** RESEARCH / ARCHITECTURE PROPOSAL — no integrated performance rig or reproducible installation is claimed  
**Creative direction:** E-Genge · Roots & Riddims · algorithmic rhythm · human-authored performance

## 1. Research question

How should GENJE organise a reproducible, live-coded audio and audiovisual environment around TidalCycles and SuperCollider while retaining human improvisation, inspectable source, timing integrity, cultural context and the ability to perform without a proprietary cloud service?

This document narrows the current livecoding research. It does not replace the movement/music interoperability or choreohacking specifications.

## 2. What the tools actually do

### TidalCycles

TidalCycles is a pattern language embedded in Haskell for composing and transforming rhythmic and musical patterns. The official documentation describes a pattern library, an editor/interpreter and an audio engine as separate connected components. Tidal can control SuperDirt by default, or other synthesis systems through OSC or MIDI.

It is therefore not a standalone audio engine and should not be described as one.

### SuperCollider

The upstream project describes SuperCollider as an audio server, programming language and IDE for sound synthesis and algorithmic composition. Its principal components include:

- `scsynth`: real-time audio server and unit-generator processing.
- `supernova`: alternative server with parallel DSP support.
- `sclang`: interpreted language used to control the server.
- `scide`: editing environment for `sclang`, with an integrated help system.
- `SuperDirt`: the common Tidal-facing synth/sampler layer, started from SuperCollider.

SuperCollider is more than a plugin or audio output device: it is the synthesis and server environment that Tidal can control.

## 3. Proposed component topology

```text
Human performer
   |
   +--> Emacs / chosen editor
   |       |
   |       +--> Tidal pattern source
   |       +--> Haskell interpreter / Tidal runtime
   |                    |
   |                    +--> OSC / MIDI
   |                             |
   |                             v
   +--> SuperCollider IDE / sclang
             |
             +--> SuperDirt
             |
             +--> scsynth or supernova
                          |
                          v
                    Audio interface
                          |
                          v
                   Sound / performance

Separate visual path:
Tidal / OSC / MIDI / authored event stream
          |
          v
Visual engine / compositor / projection
          |
          v
Audience-facing audiovisual output
```

This is a logical topology. Actual process placement, ports, audio devices, visual engine and clock synchronisation must be documented for each tested installation.

## 4. Main IDE decision: keep authoring and synthesis roles distinct

The current preferred authoring environment is Emacs, consistent with the wider WARENA practice. It is a candidate host for Tidal editing and REPL interaction, subject to verifying the current Tidal Emacs integration and package versions.

SuperCollider's own `scide` remains useful for:
- editing and evaluating `sclang`;
- booting and inspecting the audio server;
- starting and debugging SuperDirt;
- browsing built-in help and examples.

Do not force the entire workflow into one editor. A practical setup can use Emacs as the primary composition and project environment while retaining `scide` for synthesis-side development and diagnostics. This is a proposed division of responsibility, not a claim that the integration is installed or tested.

## 5. Timing, synchronisation and failure handling

A live performance system has more than one timing domain:
- Tidal pattern cycle and scheduler;
- OSC/MIDI message timing;
- SuperCollider server block and sample clocks;
- audio-device clock;
- visual engine frame clock;
- display/projector refresh;
- external movement or sensor clock, if explicitly used.

For each integration, record:
- software versions and exact source commits;
- sample rate, block size and audio device;
- Tidal control and scheduling configuration;
- OSC address/port and message format;
- latency and clock assumptions;
- visual frame rate and clock source;
- start/stop order and recovery steps;
- observable behaviour when a process, device or network link fails.

Do not claim audiovisual synchrony because two applications run on the same machine. Measure alignment with a repeatable test signal or event marker and report the method, sample count and error distribution.

## 6. GENJE composition and cultural method

The technical system should support, not define, the musical practice.

Research and composition areas:
- Genge-rooted rhythmic structures and contemporary Kenyan popular music;
- polyrhythm, repetition, variation, call-and-response and pattern transformation;
- original samples, synthesis and performer-authored material;
- NeoSoul, Reggae, Dancehall and electronic sound design;
- interaction between rhythm, gesture, movement and visual form.

Every composition or performance record should identify human authors, collaborators, source material, sample licences, cultural context, tool versions and permissions. Do not treat community music or recordings as unowned training or sample material.

## 7. Audiovisual and choreohacking integration

A later integration can expose a bounded event stream to visual or movement systems. Keep these separate:
- musical pattern representation;
- audio synthesis and rendering;
- visual event representation;
- movement notation and analysis;
- human performance decisions.

A Tidal pattern is not automatically a Laban movement score. A motion-capture stream is not automatically choreography. Any mapping between them needs a documented semantic model, explicit timing conversion and performer review.

## 8. Reproducible project layout — proposal

```text
genje-performance/
├── README.md
├── project.scm                 # if a Guix environment is validated
├── channels.scm                # pinned Guix channels, if used
├── tidal/
│   ├── patterns.tidal
│   └── README.md
├── supercollider/
│   ├── boot.scd
│   ├── synths/
│   └── README.md
├── audiovisual/
│   ├── event-schema.md
│   └── README.md
├── scores/
├── assets/
│   └── RIGHTS-AND-PROVENANCE.md
└── performance-record.md
```

This is a suggested structure, not an existing repository tree. Pin exact versions only after a working environment is built. Do not commit copyrighted samples, private recordings or credentials.

## 9. Validation work packages

| Work package | Test | Evidence required |
|---|---|---|
| WP1 — Tidal baseline | Run a minimal pattern through the selected audio backend | Versions, command sequence, audible result, logs |
| WP2 — SuperCollider baseline | Boot server and SuperDirt; evaluate a minimal synth | Server configuration, device, sample rate, logs |
| WP3 — OSC control | Send and receive a bounded test pattern | Message schema, port, timestamps, loss and latency |
| WP4 — Emacs workflow | Edit, evaluate, stop and recover a Tidal session | Exact package/configuration and reproducible steps |
| WP5 — Audio stability | Sustained performance under representative load | xruns, CPU, memory, temperature, dropout count |
| WP6 — Visual timing | Align a generated event marker with visual output | Clock mapping, measured skew and jitter |
| WP7 — Movement bridge | Map a deliberately authored event to a movement cue | Semantic mapping, performer review and notation limits |

No work package is marked complete by this research note.

## 10. Sources

Accessed 27 November 2026.

1. TidalCycles, **Documentation Reference**: https://tidalcycles.org/docs/
2. TidalCycles, **Start Tidal** — component topology and SuperDirt startup: https://tidalcycles.org/docs/getting-started/tidal_start/
3. SuperCollider project, **upstream repository and component overview**: https://github.com/supercollider/supercollider
4. SuperCollider online documentation: https://doc.sccode.org/
5. GENJE, **Algorave Guidelines and Livecoding Reference**: `algorave-guidelines-and-livecoding-reference-2026-11.md`.
6. GENJE, **Movement and Music Interoperability Study**: `GENJE-MOVEMENT-MUSIC-INTEROPERABILITY-STUDY-2026-11-20.md`.
7. GENJE, **Movement IR and Motion Research**: `GENJE-MOVEMENT-IR-AND-MOTION-RESEARCH-2026-11-20.md`.

## 11. Status and next decisions

- **VERIFIED FROM UPSTREAM DOCUMENTATION:** TidalCycles' pattern/interpreter/audio-engine separation; SuperCollider's server/language/IDE components.
- **PROPOSED:** Emacs as primary authoring environment with SuperCollider IDE retained for synthesis development.
- **UNKNOWN / TO TEST:** exact Guix package availability and versions, Emacs Tidal integration, audio interface compatibility, OSC routing, performance latency and audiovisual synchronisation.
- **NOT CLAIMED:** a finished GENJE IDE, installed live rig, public performance, validated latency or integrated choreohacking system.

Next: audit the current GENJE and WARENA Guix package candidates, build a minimal reproducible Tidal → SuperDirt → SuperCollider session, and record the actual environment before selecting the long-term IDE arrangement.

---

**GENJE ZA WARENA · GLORY / EXPRESSION**  
**Human authorship · Sound · Rhythm · Movement · Code**

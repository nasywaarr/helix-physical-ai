# Helix — Physical AI Study & 3D Asset Pipeline

> Analyzing Figure AI's **Helix** Vision-Language-Action model, and building a humanoid robot asset in Blender → USD, ready for NVIDIA Omniverse simulation.

**Course:** Devices and Circuits for AI · Università degli Studi di Messina  
**Author:** Nasywa Azzahra Rizqi Ramadhani (574106)  
**Supervisor:** Prof. Giovanni Finocchio

---

## Overview

This project explores **Physical AI** through the lens of Figure AI's **Helix** — a Vision-Language-Action (VLA) model that unifies perception, language understanding, and learned control on real humanoid robots.

It has two parts:

1. **A study & presentation** analyzing how Helix works and why it matters for AI hardware.
2. **A 3D asset pipeline** — a humanoid robot modeled in Blender and exported to **USD** (`.usdc`), prepared for physics simulation in NVIDIA Omniverse. The concept: a robot that handles grocery items and places them into a fridge, mirroring Figure's real Helix demo.

---

## What is Helix?

Helix is a VLA model developed in-house by Figure AI. It takes in **camera pixels + natural-language commands** and outputs **robot actions** directly — no task-specific scripting.

Its key idea is a **dual-system architecture** inspired by human "System 1 / System 2" cognition:

| System | Role | Size | Rate |
|--------|------|------|------|
| **System 2 (S2)** | Slow "thinker" — scene understanding & language | 7B params (VLM) | 7–9 Hz |
| **System 1 (S1)** | Fast "reflex" — real-time motor control (35 DOF) | 80M params | 200 Hz |

**Why split them?** VLMs are *general but slow*; motor policies are *fast but not general*. Decoupling lets each run at its optimal timescale — while both are trained **end-to-end**.

**Why it matters for hardware:** Helix runs entirely on **onboard embedded GPUs** — no cloud. A 200 Hz control loop can't tolerate network latency, and safety demands local compute. This is Physical AI: where the model meets the circuits and devices that let it act in the real world.

---

## The 3D Asset Pipeline

![Humanoid robot modeled in Blender](assets/helix%20blender.png)

*The humanoid robot modeled in Blender, in T-pose with a Catmull-Clark subdivision modifier applied.*

| Stage | Tool | Output |
|-------|------|--------|
| Modeling | Blender (Catmull-Clark subdivision) | Humanoid mesh |
| Export | USD | `helix.usdc` (binary crate format) |
| Simulation | NVIDIA Omniverse | Physics-ready digital twin |

**Why USD?** Pixar's Universal Scene Description is the standard 3D interchange format and the native format of Omniverse. The `.usdc` binary "crate" variant is compact and fast to load (vs. `.usda` ASCII or `.usdz` package).

**Why simulate?** *Sim-to-real* — behaviors like grabbing and placing groceries can be tested safely and cheaply in a digital twin before touching real hardware.

---

## Repository Structure

```
.
├── README.md
├── LICENSE
├── presentation/
│   └── Physical AI Presentation.pdf
└── assets/
    ├── helix.usdc            # USD export, Omniverse-ready
    └── helix blender.png     # Blender viewport reference
```

---

## Tools & Tech

`Blender` · `Universal Scene Description (USD)` · `NVIDIA Omniverse` · Figure AI **Helix** (VLA)

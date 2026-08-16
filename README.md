# The Sunless Basilica — Subterranean Level Design & Technical Environment

An atmospheric third-person subterranean level design and real-time environment created in Unreal Engine 5. This project focuses on environmental storytelling, dynamic lighting pipelines, procedural world-building, and spatialized ambient soundscapes—guiding the player from an overgrown daylight entrance into a dark, ancient underground sanctuary.

---

## 1. Project Overview

**The Sunless Basilica** is a level design and technical environment art showcase exploring scale, lighting transitions, and player routing through subterranean architecture. 

The environment takes the player on a continuous journey:
* **Daylight Approach**: An open, natural rock clearing that grounds the player scale and introduces the environment.
* **The Descent & Temple Ruins**: Tight corridors and ancient stone halls lit by dynamic torchlight, shifting the tone into darkness.
* **The Inner Shrine**: A vast, flooded underground cavern featuring colossal pillars, floating ancient relics, and subtle skylight fissures.

---

## 2. Core Disciplines & Technical Pillars

### Landscape & Terrain Generation
* Sculpted custom subterranean terrain and high-cliff rock walls to establish strong natural sightlines and organic boundaries.
* Built multi-layer landscape materials blending mossy terrain, rough rock surfaces, and aged subterranean stone pavement.
* Designed natural verticality and choke points to control pacing and reveal key architectural landmarks progressively.

### Procedural Content Generation (PCG) & Foliage
* Implemented PCG Graphs to distribute surface debris, scattered dry autumn leaves, and foliage patches dynamically across stone corridors.
* Applied density masks and distance-based falloffs to keep primary traversal paths clean while clustering debris naturally around column bases and crevices.
* Injected rotation and scale randomization across static meshes to eliminate repetitive patterns in large modular assets.

### Dynamic Lighting & Atmosphere (Lumen)
* **High-Contrast Palette**: Designed a smooth temperature transition from cold 6500K outdoor daylight to warm 2400K torch firelight in the corridors, culminating in cool desaturated tones within the flooded inner shrine.
* **Dynamic Point & Spot Lights**: Tuned realistic inverse-square falloffs, attenuation radii, and dynamic shadow casting on wall sconces and the player's handheld torch.
* **Volumetric Fog & God Rays**: Configured Exponential Height Fog and local scattering multipliers to capture airborne dust particles and light beams cutting through rock fissures.

### Ambient Sound & Audio Spatialization
* **Sound Cue Layering**: Combined outdoor breezes with low subterranean rumbles, distant water droplets, and interior stone reverb.
* **3D Spatial Attenuation**: Positioned localized 3D audio emitters on burning torches, braziers, and falling water streams to reinforce directional environmental cues.
* **Reverb & Occlusion**: Configured audio volumes with custom low-pass filtering and cave reverb presets to transition smoothly between open spaces and tight corridors.

---

## 3. Challenges & Technical Solutions

### Lighting: Lumen Surface Cache Oversubscription & Leaks
* **Challenge**: Dense rock meshes and repeating modular architecture caused Lumen surface cache oversubscription, leading to shadow pop-in and light bleeding through thin wall seams.
* **Solution**: 
  * Increased the global surface cache atlas ceiling via `r.Lumen.ScreenProbeGather.SurfaceCache.AtlasSize 4096`.
  * Placed exterior shadow-caster blocking geometry behind cave seams to eliminate light bleed.
  * Optimized mesh card generation by lowering Lumen detail trace distance on non-critical background assets.

### Sound: Audio Bleed & Spatial Transitions
* **Challenge**: Outdoor ambient sounds bled into deep underground tunnels, and interior reverb triggered too abruptly.
* **Solution**:
  * Established bounded Audio Volumes across entrance thresholds with a 1.5s crossfade duration.
  * Adjusted LPFIgnore and applied dedicated interior submix presets to achieve natural acoustic dampening as the player descends.

---

## 4. Level Walkthrough & Flow

The player experience is structured as a single continuous progression through five distinct spatial beats:

1. **The Daylight Threshold**: Introduces the player to the outer rock clearing, setting baseline navigation, player scale, and exterior audio tones.
2. **The Ruined Portal**: A monumental ancient archway where lighting smoothly drops from bright 6500K daylight into warm 2400K torchlight, signaling the transition underground.
3. **Subterranean Courtyard**: A wide subterranean architectural hall guarded by elephant statues, open braziers, and procedural ground debris.
4. **Descent Staircase**: A narrow, vertical stone stairway that compresses player sightlines and introduces localized cave reverb and falling dust.
5. **The Sunless Basilica**: The level's climax—a vast flooded sanctuary with towering monolithic pillars, reflective water surfaces, and an ancient relic floating beneath a fractured ceiling skylight.

---

## 5. Technical Specifications

| Feature | Configuration / Tool |
| :--- | :--- |
| **Engine** | Unreal Engine 5 |
| **Global Illumination** | Lumen Dynamic GI & Reflections |
| **Geometry** | Nanite Virtualized Meshes |
| **World Building** | Unreal Landscape Tools + PCG Framework |
| **Lighting** | Dynamic Directional Light + Point/Spot Lights + Volumetric Height Fog |
| **Audio** | Unreal Audio Engine (3D Attenuation + Reverb Audio Volumes) |

---

## 6. How to Run the Project

1. Clone the repository:
   ```bash
   git clone [https://github.com/ChiraagRokade/TheSunlessBasilica.git](https://github.com/ChiraagRokade/TheSunlessBasilica.git)
# Regni MIDI DAW (working title)

A **MIDI-only** DAW, built for people who compose with sample libraries, mainly virtual orchestra.
It does not try to compete with Logic, Cubase or Pro Tools on audio. It does one thing: get out of the composer's way
the problems that general-purpose DAWs never solved, because their focus was elsewhere.

Status: **idea written down on 2026-10-25, nothing implemented yet.** The full idea is in [IDEA.md](IDEA.md).

## In one sentence
The grid shows the **musical intention**. The DAW takes care of the libraries' physics: per-articulation latency,
keyswitches, CCs and template loading.

## Relation to the other Regni products
- **Regni Ensemble** is the engine: it hosts the instruments, runs the Switchboard (articulations) and the Latency
  layer. The DAW is a front end that talks to it, and does not rewrite any of that.
- The philosophy of every Regni product: **ready-made presets**, per library and per instrument, and the user
  **customizes everything and saves their own presets**.

A map of all the problems and where each solution lives (plugin / Ensemble / MIDI DAW) is kept in the Regni Ensemble
documentation (`docs/MAPA-DE-PROBLEMAS.md`).

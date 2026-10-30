# The idea: a MIDI-only DAW for virtual orchestra

> Written down on 2026-10-25, from a conversation with Sergio during the redesign of the Regni Ensemble Switchboard.
> Nothing here is implemented. Claims about what other DAWs do are marked **(verify)**.
> They must be checked against each DAW's manual (primary source) before they become product arguments.

## Why it should exist

The most popular DAWs grew around audio recording, mixing, and band and electronic production. People who write
for virtual orchestra spend the day fighting problems that, for this audience, are the core of the job:

## The problems it tackles

### 1. Articulation latency (the main problem)
Each articulation of a sample library takes a different time to "speak". A string legato can take
~200–300 ms; a staccato, almost nothing. And it is not a fixed number: it varies with

- the **transition**: the first note of a legato responds quickly, while a *connected* note takes longer;
- velocity and dynamics (CC1);
- the keyboard region;
- the library and the patch.

**Live playing can be improved** (see the Latencinator, in the Regni MIDI FX line): a Low Latency mode (the library
starts the sample later, e.g. Pacific CC14 → LV), fast vs realistic patch, compensation of the first legato note,
by velocity and by dynamics. The price is realism; that is why these are modes (Low Latency / Realistic / the
library's Default), switched with a single button, independent of the transport.

**What happens today without this.** The musician **plays early, by ear**. The DAW records the note where the key
was pressed, that is, early and off the grid. The common workaround is a negative *track delay*, which only acts on
playback and is one number per track, not per articulation **(verify: Logic, Cubase, Studio One, Dorico, Reaper)**.
The composer ends up quantizing and dragging notes by hand.

**What we want.**
- **Record the note where it sounded**: the moment of the key press plus the delay of that articulation in that
  situation. The note lands on the grid the way the musician meant it.
- **On playback, send the note early** by exactly the same amount.
- The grid shows the musical intention, and the library's physics stays hidden.
- An option for people who do *not* play early (then there is no compensation when recording, only on playback).
- Recording in Low Latency and playing back in Realistic already puts the note almost on the grid; the DAW corrects
  the remainder.
- The delays come from **ready-made presets per library** (measured by us), with rules (transition, velocity,
  dynamics, region), and the user edits them and saves their own.

This **cannot be done with a plugin alone** inside another DAW: the DAW records the MIDI before the plugin receives
it. It is the main reason for this product to exist.

### 2. Per-note articulation, painless
Switching articulations today means setting up articulation sets or expression maps tied to the DAW and the library,
built by hand or bought ready-made and fixed (Babylonwaves) **(verify what each DAW already offers per note)**.

What we want, following the same three-layer logic as the Ensemble Switchboard:
- **Palette:** your articulations, with your names and keys, customizable, with several palettes;
- **Instrument:** what the library really has;
- **Connections:** the cable between the palette and the instrument, with ready-made presets.

Also: articulation as a property of the note in the piano roll, not keyswitch notes cluttering the roll.

### 3. State "chase" when starting in the middle
Starting playback in the middle of the piece and hearing the wrong articulation or CC, because the last keyswitch or
CC was before the start point **(verify how each DAW chases keyswitches)**. The DAW should always know and send the
right state of each instrument at any point.

### 4. Huge templates
Orchestral templates with hundreds of instruments are slow to open, heavy on RAM, and bog the project down. Regni
Ensemble already hosts the instruments outside the DAW. Here it becomes native: the template is loaded once and the
project only points to it.

### 5. CCs designed for orchestra
Dynamics (CC1), expression (CC11) and vibrato drawn as musical curves. Things like "this whole section does a
crescendo", and adjusting the dynamics of several lines together.

## What it MUST have even though it is "MIDI only"
- tempo map and time signature changes;
- **video sync**, because the audience writes film and media music;
- stem export (audio rendering, done by the Ensemble);
- a first-class piano roll and MIDI editing.

## What it does NOT do (on purpose)
- audio recording, comping, vocal editing;
- deep mixing (at most levels and stems);
- chasing every feature of a general-purpose DAW.

## Open questions
- How do we measure the delay of each articulation of each library (automatically, by analysing the rendered audio?).
- The format of the latency and palette presets, shareable between products and between users.
- Notation: integrate with Regni Notação or stay with the piano roll only?
- Platform: macOS only at first? JUCE, like the Ensemble?
- Product name.

## Before starting to build
1. Read the manuals (Logic, Cubase, Studio One, Dorico, Reaper) and confirm or refute each **(verify)** above.
2. Have the Ensemble's Latency layer and Switchboard finished and tested in real use. They are the engine.

# EzBeat

EzBeat is a minimal C++ command-line synthesizer that generates 16-bit mono WAV files.

This repository contains:

- `ezbeat.cpp` — full, readable source version
- `ezbeat_small.cpp` — compact/minified version with identical functionality

The program can:

- Generate a built-in demo melody
- Generate audio from a custom input file
- Output either a clean sine wave or a "nostalgic" lo-fi style tone
- Optionally apply an exponential fade envelope

---

## Build

### Compile full version

```bash
g++ ezbeat.cpp -o ezbeat
```

### Compile compact version

```bash
g++ ezbeat_small.cpp -o ezbeat_small
```

---

## Usage

### Full version

```bash
./ezbeat -o=output.wav (-i=input.txt | -demo) [-type=clean|nostalgic] [-mode=fade|nfade]
```

### Compact version

```bash
./ezbeat_small -o=output.wav (-i=input.txt | -demo) [-type=clean|nostalgic] [-mode=fade|nfade]
```

---

## Required Arguments (choose one)

- `-demo`  
  Runs the built-in demo melody.

- `-i=<file>`  
  Reads pitch and timing data from an input file.

You must specify exactly one of these options.

---

## Optional Arguments

- `-o=<file>`  
  Output WAV file name (default: `daisy.wav`)

- `-type=clean`  
  Pure sine wave synthesis

- `-type=nostalgic`  
  Lo-fi styled tone with modulation, noise, and filtering

- `-mode=fade`  
  Applies exponential amplitude decay (default behavior)

- `-mode=nfade`  
  Disables amplitude decay

- `-h`  
  Show help message

---

## Input File Format

The input file must contain two lines:

```text
pitches: 69,71,72
time: 1,1,2
```

- `pitches` — MIDI note numbers
- `time` — duration multipliers

The number of pitches must match the number of time values.

Durations are internally scaled by a fixed quarter-note constant.

---

## Output Format

- WAV (RIFF)
- 16-bit PCM
- Mono
- 4000 Hz sample rate

# Concat Synth

A browser-based concatenative synthesizer that reconstructs a target sound using chunks from a source sound.

## How It Works

1. **Load a target sound** — the sound you want to recreate
2. **Load a source sound** — the material to build from
3. **Synthesize** — the algorithm analyses both sounds, then reconstructs the target by finding the best-matching source chunk for each target chunk

The matching is based on audio features extracted from both time and frequency domains.

## Features Analysed Per Chunk

**Time domain:**
- RMS energy (loudness)
- Zero-crossing rate (brightness/noisiness indicator)

**Frequency domain:**
- Spectral centroid (timbral brightness)
- Spectral flatness (how noise-like vs tonal)
- MFCCs (13 coefficients — timbral shape)
- Binned magnitude spectrum (32 bands)

## Controls

| Control | Description |
|---------|-------------|
| **Chunk Size (ms)** | Window size for analysis and synthesis. Smaller = more granular, larger = smoother |
| **FFT Size** | Resolution of frequency analysis (256–8192) |
| **Overlap %** | How much consecutive chunks overlap in regular mode |
| **Mode** | Regular (overlapping chunks) or Transients (onset-aligned chunks) |
| **Sensitivity** | Transient detection threshold (lower = more transients detected) |
| **Fade Out %** | Percentage of chunk length to fade out at the end |
| **Crossfade (ms)** | Crossfade duration between consecutive chunks |

## Modes

### Regular Mode
Extracts overlapping chunks at fixed intervals across the entire sound. Good for:
- Textural transformations
- Sustained/ambient sounds
- Dense polyphonic material

### Transient Mode
Detects onsets (attacks) and only extracts chunks starting at transients. Good for:
- Drum replacement
- Percussive material
- Preserving rhythmic structure

The transient detector uses an adaptive threshold based on the RMS envelope's first derivative.

## Tips

- **Short chunks (20–40ms)** produce glitchy, granular textures
- **Longer chunks (100–200ms)** give smoother, more coherent results
- **Higher overlap** in regular mode creates smoother transitions
- **Fade out** is useful for creating staccato or gated effects
- **Crossfade** smooths transitions, especially audible in transient mode
- Works best when source material has similar spectral variety to the target
- Click any cell in the **chunk map** to audition that source chunk

## Chunk Map Visualisation

After synthesis, a grid shows which source chunks were used:
- **Colour** = position in source file (hue maps to time)
- **Brightness** = match quality (brighter = better match)
- **Click** any cell to play that chunk

## Usage

1. Drag and drop audio files onto Target and Source zones (or click to browse)
2. Adjust parameters as needed
3. Click **Synthesize**
4. Use play buttons to audition target, source, or result
5. Click **Download WAV** to export

The **swap button** (↔) between target and source lets you quickly reverse the direction.

## Browser Requirements

- Modern browser with Web Audio API support
- Tested in Chrome, Firefox, Safari

# GNU Radio Stereo FM Matrix TX/RX Experiment

Modern GNU Radio Companion stereo FM matrix transmit/receive DSP experiment.

This public repository is split from the audited `modern-gnuradio-sdr-flows` workspace. It keeps a focused GNU Radio Companion flow family with archived originals in `flows/` and validated modern ports in `modern/`.

## Features

- Stereo FM matrix encode/decode experiment
- Pilot/subcarrier signal-source paths modernized from legacy constants
- WAV/file source paths preserved
- Audio sink monitoring
- Legacy pre-3.7 graph modernized beside the later graph

## Standards and Signal Context

- FM stereo multiplex concepts: L+R, L-R, 19 kHz pilot, 38 kHz suppressed subcarrier
- GNU Radio Companion XML validated with GNU Radio 3.8.5.0

## Flowgraph Inventory

| Flowgraph | Blocks | Connections | Key Parameters | Hardware/Audio Blocks | Transmit Blocks |
| --- | ---: | ---: | --- | --- | --- |
| `stereofmtxrx.grc` | 62 | 67 | - | audio_sink_0 (audio_sink) | - |
| `stereofmtxrx.grc.legacy-modernized` | 62 | 67 | - | audio_sink_0 (audio_sink) | - |

## File and Capture Paths

- `stereofmtxrx.grc`: gr_wavfile_source_0.file=/home/testmusic48KHz.wav; gr_file_source_0.file=/home/iqf.dat
- `stereofmtxrx.grc.legacy-modernized`: gr_wavfile_source_0.file=/home/testmusic48KHz.wav; gr_file_source_0.file=/home/iqf.dat

Update these paths before running graphs on a different machine. Generated files, captures, recordings, and raw samples are intentionally ignored by git.

## Usage Examples

```sh
# Validate modernized flowgraphs
/opt/local/Library/Frameworks/Python.framework/Versions/3.9/bin/python3.9 tools/validate_grc.py modern/* --report VALIDATION.md

# Generate Python without running RF hardware
mkdir -p generated
for f in modern/*; do /opt/local/bin/grcc -o generated "$f"; done

# Verify committed file integrity
shasum -a 256 -c SHA256SUMS.txt
```

To open a graph interactively:

```sh
gnuradio-companion modern/<flowgraph>.grc
```

To run generated Python, inspect the generated script first and confirm hardware, frequency, gain, sample rate, and file paths. Do not run transmit-capable graphs directly from generated code without RF isolation and legal authorization.

## Safety

DSP/audio experiment in this split; update old `/home/...` source paths before running.

## Audit Status

- Archived originals parse as XML. See `AUDIT.md`.
- Modernized flowgraphs validate OK. See `VALIDATION.md`.
- Python generation was verified with GNU Radio Companion Compiler 3.8.5.0. See `COMPILE.md`.
- Checksums are tracked in `SHA256SUMS.txt`.

## Repository Layout

- `flows/` - archived original flowgraphs and related data files.
- `modern/` - modernized GNU Radio Companion flowgraphs for normal use.
- `tools/` - repeatable audit and validation helpers.
- `README.md` - usage and technical overview.
- `DESCRIPTION.md` - short project description.
- `AUDIT.md`, `VALIDATION.md`, `COMPILE.md` - generated audit/verification reports.

## License

No new license is asserted for the archived flowgraphs. Preserve original ownership/history before redistribution or publication.

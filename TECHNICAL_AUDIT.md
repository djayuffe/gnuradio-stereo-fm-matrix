# Technical Audit

This audit covers the modern-only public repository `gnuradio-stereo-fm-matrix`.

## Scope

- Modern flowgraphs audited: 2.
- Outdated public XML removed from the repo.
- Repo-local file paths used for samples/captures.
- GNU Radio Companion validation target: 3.8.5.0.

## Tooling Review

- `tools/audit_flows.py` parses GRC XML, hashes each file, reports block/connection counts, hardware endpoints, transmit-capable sinks, file paths, duplicate IDs, and exact duplicate payloads.
- `tools/validate_grc.py` uses GNU Radio Companion's Python API to load, rewrite, and validate each modern `.grc`; it does not rely on ad hoc text matching.
- Setup scripts, where present, create safe placeholder local files only. They do not run SDR hardware.

## Feature and Parameter Coverage

| Flowgraph | Blocks | Connections | Key Parameters | Hardware/Audio Blocks | Transmit Blocks |
| --- | ---: | ---: | --- | --- | --- |
| `stereofmtxrx.grc` | 62 | 67 | - | audio_sink_0 (audio_sink) | - |
| `stereofmtxrx.variant.grc` | 62 | 67 | - | audio_sink_0 (audio_sink) | - |

## File Path Coverage

- `stereofmtxrx.grc`: gr_wavfile_source_0.file=samples/testmusic48KHz.wav; gr_file_source_0.file=samples/iqf.dat
- `stereofmtxrx.variant.grc`: gr_wavfile_source_0.file=samples/testmusic48KHz.wav; gr_file_source_0.file=samples/iqf.dat

## Remaining Runtime Responsibilities

- GRC validation and `grcc` generation do not prove connected SDR/audio hardware behavior.
- Users must configure local devices, antennas, sample files, and gains.
- Transmit-capable graphs require RF isolation and authorization before any runtime use.

## Verification Checklist

- `VALIDATION.md` contains no `Result: FAILED` entries.
- `SHA256SUMS.txt` verifies all committed files.
- Generated Python and runtime captures remain ignored by git.

# Technical Audit

This audit summarizes code, functions, and feature coverage for `gnuradio-stereo-fm-matrix`.

## Scope

- Flowgraphs audited: 2 modern files plus archived originals in `flows/`.
- Tools audited: `tools/audit_flows.py` and `tools/validate_grc.py`.
- Reports regenerated locally before publication.

## Code and Function Review

- `tools/audit_flows.py` parses XML with `xml.etree.ElementTree`, hashes each file, lists block counts, connection counts, hardware endpoints, transmit-capable sinks, explicit file paths, duplicate block IDs, and exact duplicate payloads.
- `tools/validate_grc.py` uses the installed GNU Radio Companion core API, not text matching, to load, rewrite, and validate each modern `.grc` file.
- Shell examples avoid executing generated RF graphs automatically; generation and validation are separate from runtime operation.

## Feature Coverage

- Stereo FM matrix encode/decode experiment
- Pilot/subcarrier signal-source paths modernized from legacy constants
- WAV/file source paths preserved
- Audio sink monitoring
- Legacy pre-3.7 graph modernized beside the later graph

## Technical Parameters

| Flowgraph | Blocks | Connections | Key Parameters | Hardware/Audio Blocks | Transmit Blocks |
| --- | ---: | ---: | --- | --- | --- |
| `stereofmtxrx.grc` | 62 | 67 | - | audio_sink_0 (audio_sink) | - |
| `stereofmtxrx.grc.legacy-modernized` | 62 | 67 | - | audio_sink_0 (audio_sink) | - |

## Known Operational Gaps

- Runtime hardware behavior is not asserted by validation; actual SDR/audio devices must be configured locally.
- External sample/capture files named in legacy graphs are not bundled unless present in `flows/`.
- Transmit-capable graphs require separate RF lab controls and legal authorization.

## Verification

- `VALIDATION.md` has no `Result: FAILED` entries.
- `SHA256SUMS.txt` verifies all committed files.

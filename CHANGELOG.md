# Changelog

**Language:** English | [日本語](CHANGELOG.ja.md)

All notable public changes to VoluBridge are recorded here.

## [1.0.0] - 2026-05-11

Initial release.

### Added

- Menu bar app for routing macOS audio through `VoluBridgeRT` to a selected real output device.
- Bundled CoreAudio HAL driver installation, update, and removal from inside the app.
- Keyboard volume control for external outputs such as HDMI monitors, DisplayPort monitors, USB DACs, audio interfaces, and headphones.
- Separate `System Output` and `VoluBridge Output` device selection.
- Automatic direct-output behavior when macOS is set to a physical device instead of VoluBridge.
- Fine-grained volume steps.
- Output channel-pair selection for multi-channel devices.
- Real-time VU meter, spectrum view, and OPTIMIZER section.
- Advanced RT controls for sample rate, clock behavior, buffers, fixed target, reported latency, reported safety, and power-saving behavior.
- RT Diagnostics with counters and state for sync, underflow, device switching, buffer behavior, clock tracking, and routing health.
- English and Japanese localization.
- 14-day trial, license-key activation, signed license lease handling, and license validation.
- In-app update check for VoluBridge releases.

### Notes

- First-time driver installation and driver updates require administrator approval because the CoreAudio HAL driver is installed under `/Library/Audio/Plug-Ins/HAL`.

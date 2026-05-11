# VoluBridge

**Language:** English | [日本語](README.ja.md)

**Website:** [VoluBridge Official Website](https://bridgedevs.com/volubridge)

VoluBridge is a macOS menu bar app for controlling external audio outputs with the normal keyboard volume keys.

It is designed for HDMI and DisplayPort monitors, USB DACs, audio interfaces, headphones, and other output devices that macOS can play through but cannot always control with the system volume keys.

## What VoluBridge Does

VoluBridge adds a virtual CoreAudio output device called `VoluBridgeRT`. macOS sends audio to that virtual device, and VoluBridge routes it to the real speaker, monitor, DAC, or interface you choose.

In everyday use, this means:

- choose `VoluBridge` as the macOS system output
- choose your real device in the VoluBridge menu bar panel
- use the keyboard volume keys as usual

If you select a physical output directly in macOS, VoluBridge automatically treats that path as direct output instead of forcing all audio through the bridge.

## Highlights

- Keyboard volume control for HDMI, DisplayPort, USB, and other external outputs
- Menu bar control panel with separate `System Output` and `VoluBridge Output` sections
- Bundled CoreAudio HAL driver, installed and updated from inside the app
- Fine-grained volume steps for more precise control
- Output channel-pair selection for multi-channel devices
- Automatic handling for sleep, reconnects, output switching, and sample-rate changes
- Real-time VU meter, spectrum view, and OPTIMIZER section
- RT diagnostics for sync, underflow, buffer, clock, and routing state
- English and Japanese UI
- 14-day trial with license activation

## Requirements

- macOS 11 or later
- Apple Silicon Mac
- Administrator password for first-time driver installation or driver updates

## Installation

1. Download the VoluBridge DMG from the release package.
2. Drag `VoluBridge.app` into `/Applications`.
3. Launch `VoluBridge.app`.
4. Follow the first-launch prompt to install the bundled `VoluBridgeRT.driver`.
5. Enter your administrator password when macOS asks for it.

The driver is bundled inside the app. You do not need to run a separate companion process.

## Basic Use

1. Open the VoluBridge icon in the menu bar.
2. Under `System Output`, select `VoluBridge`.
3. Under `VoluBridge Output`, select the real device you want to hear.
4. Use the keyboard volume keys or the macOS volume slider.

The top status shows the current route:

- `<device name> (VoluBridge)` means audio is routed through VoluBridge.
- `<device name> (Direct)` means macOS is sending audio directly to that device.

## Advanced Controls

Most users can keep the defaults. Advanced Settings are available for setups that need explicit tuning, such as DAWs, video editing systems, unstable HDMI paths, or devices with unusual buffer behavior.

Advanced controls include sample-rate behavior, clock mode, fixed target, virtual and device buffers, reported latency and safety values, power-saving behavior, and RT diagnostic counters.

## License

VoluBridge includes a 14-day trial. After purchase, use `Enter License Key` in the app to activate the full version.

License activation uses a Machine ID for seat management and support. Audio routing and analysis are handled locally on the Mac.

## Support

See [SUPPORT.md](SUPPORT.md) for troubleshooting steps and the information to include when reporting a problem.

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for release notes.

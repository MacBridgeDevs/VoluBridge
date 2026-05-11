# VoluBridge

**Language:** English | [日本語](README.ja.md)

**Website:** [VoluBridge Official Website](https://bridgedevs.com/en/volubridge)

**Download:** [Latest DMG](https://bridgedevs.com/volubridge/releases/latest) | [FAQ](https://bridgedevs.com/en/volubridge/faq) | [Reference](https://bridgedevs.com/en/volubridge/reference)

VoluBridge is a CoreAudio-based volume bridge for Apple Silicon Macs. It lets HDMI monitors, DisplayPort monitors, USB-C displays, USB DACs, audio interfaces, headphones, and other macOS output devices work with the normal Mac volume keys.

No DDC dependency. No always-open app requirement. The audio bridge runs at the driver level; the app is the control panel for output selection, EQ, VU meters, FFT, RT diagnostics, and driver management.

![VoluBridge app showing volume control, meters, and optimizer](https://bridgedevs.com/VoluBridgeCapture.png)

## Why Try It

- Your external monitor plays audio, but the Mac volume keys do not control it naturally.
- Your USB DAC or audio interface is visible to macOS, but you want standard volume-key behavior.
- DDC control is unreliable, unavailable, too coarse, or not relevant to your audio path.
- You want a driver-level bridge instead of keeping a mixer or audio utility window open.
- You want to see what the audio path is doing through meters, spectrum display, and RT diagnostics.
- You want a 14-day trial to check your own monitor, DAC, dock, app, and daily workflow before buying.

## What VoluBridge Does

VoluBridge adds a virtual CoreAudio output device called `VoluBridgeRT`. macOS sends audio to that virtual device, and VoluBridge routes it to the real speaker, monitor, DAC, or interface you choose.

In everyday use, this means:

- choose `VoluBridge` as the macOS system output
- choose your real device in the VoluBridge menu bar panel
- use the keyboard volume keys as usual

If you select a physical output directly in macOS, VoluBridge automatically treats that path as direct output instead of forcing all audio through the bridge.

![VoluBridge output routing and channel selection](https://bridgedevs.com/assets/volubridge-output-routing.png)

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

## Where It Fits

If DDC volume control is stable in your setup, a DDC control app may be enough. VoluBridge is aimed at external-audio setups that DDC cannot handle well, and at users who want USB DACs or audio interfaces to behave like normal Mac outputs.

| Area | VoluBridge | DDC apps | Typical audio utilities |
|---|---|---|---|
| External monitor volume | Supported | Possible in compatible setups | Usually adjusted through an in-app mixer |
| USB DAC / audio interface volume keys | Supported | Usually out of scope | Usually focused on in-app volume or EQ |
| DDC dependency | No | Yes | No |
| HDMI / DisplayPort setups | Supported | Monitor-dependent | Treated as CoreAudio outputs, not primarily as monitor-volume control |
| Standard volume keys / HUD | Supported | Usually mapped to monitor control | Often centered on custom UI or in-app control |
| Minimum volume / volume steps | Handled as Mac-side volume control | Depends on each monitor's minimum volume and step behavior | Depends on the app's own volume processing |
| Always-open app dependency | Core output runs at driver level | Usually controlled by a resident app | Often expects a resident audio-processing app |
| Low-latency bridge design | Core focus | Out of scope | Usually focused on mixer / EQ / routing processing |
| VU / FFT / RT diagnostics | Integrated | Usually none | Often meter / EQ display; RT diagnostics are uncommon |
| Main use | External audio output bridge | Monitor control | Mixer / EQ |

## Latency Model Comparison

VoluBridgeRT is not designed as a simple FIFO path that stores audio and plays it back later. It aligns the producer schedule and render output time around a fixed target, so the virtual path is designed to avoid latency buildup during long sessions.

| Area | Typical FIFO model | VoluBridgeRT |
|---|---|---|
| Main stability strategy | Keep queued audio stock | Track the output timeline |
| Latency behavior | Changes with how much audio is buffered | Controlled around a fixed target |
| Long sessions | Delay can grow if the queue grows | Designed to avoid accumulating delay |
| Underflow recovery | Queue state can collapse and leave delay behind | Resyncs around the target timeline |
| What diagnostics show | Usually limited to buffer or app state | Fixed Cursor, Real Add Latency, missing, underflow, clock, and routing state |

This does not mean physical latency disappears. It means VoluBridge is designed not to add unnecessary waiting time over direct hardware output.

## Optimizer And Visibility

VoluBridge is not only an output switch. The app gives you practical tools for checking and shaping the output you actually hear.

- `OPTIMIZER` with 7-band EQ, presets, and SoftClipper
- Peak and RMS meters for quick loudness checks
- Spectrum display for confirming audio activity
- Compact output switching for daily use
- RT Diagnostics for sync, underflow, buffer, clock, and routing state

## Tested Setups So Far

Current checks include M1 MacBook Air, Mac Studio M4 Max, ASUS PG42UQ, M1 MacBook Air built-in audio, RME UFX, Roland Fantom 08, Cubase, Parallels Desktop, Spotify, and YouTube. Device-specific behavior can vary, so the 14-day trial is the recommended compatibility check.

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

VoluBridge includes a 14-day trial. After purchase, use `Enter License Key` in the app to activate the full version. Current pricing and license terms are listed on the [official website](https://bridgedevs.com/en/volubridge/buy).

License activation uses a Machine ID for seat management and support. Audio routing and analysis are handled locally on the Mac.

## Support

See [SUPPORT.md](SUPPORT.md) for troubleshooting steps and the information to include when reporting a problem.

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for release notes.

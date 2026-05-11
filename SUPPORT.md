# Support

**Language:** English | [日本語](SUPPORT.ja.md)

This page lists the fastest checks to make before reporting a VoluBridge problem.

## Supported Systems

VoluBridge supports macOS 11 or later on Apple Silicon and Intel Macs.

The app installs a CoreAudio HAL driver named `VoluBridgeRT.driver`. Installing, updating, or removing that driver requires administrator approval and may briefly restart CoreAudio.

## Quick Checks

### No Sound

1. Open the VoluBridge menu bar panel.
2. Confirm `System Output` is set to `VoluBridge`.
3. Confirm `VoluBridge Output` is set to the real monitor, DAC, speaker, headphones, or interface you want to hear.
4. Check that the top status says `<device name> (VoluBridge)`.
5. Run `Reset Audio Connection` from the app.

### VoluBridge Output Does Not Appear

1. Open VoluBridge and check the `Driver:` row.
2. If the driver is not installed, choose `Install Driver`.
3. If an update is available, choose the driver update item.
4. If the output still does not appear, quit and reopen VoluBridge.

### Volume Keys Do Not Work

If `Fine-grained Volume Steps` is enabled, macOS Accessibility permission is required.

After an app update, macOS can keep a stale permission entry. Use `Reset Accessibility Permission` in VoluBridge, then grant Accessibility permission again in System Settings.

### Clicks, Dropouts, or Delayed Resume

Open `RT Diagnostics` and copy the diagnostic text before changing many settings. Useful values include underflow count, fixed cursor state, last underflow context, device buffer, reported latency/safety, phase precision, and output switch errors.

For unstable HDMI displays or heavily loaded systems, try:

- `Reset Audio Connection`
- a larger fixed target or device buffer
- disabling power saving for testing
- reconnecting the display, dock, DAC, or audio interface

## Information to Include

When reporting an issue, include:

- macOS version
- Mac model and CPU type
- VoluBridge app version and build
- VoluBridge driver version and build
- output device name and connection type, such as HDMI, DisplayPort, USB, Bluetooth, dock, or interface
- whether the status shows `(VoluBridge)` or `(Direct)`
- whether the problem happens after sleep, reconnect, app launch, output switch, sample-rate change, or license activation
- copied `RT Diagnostics` text when audio glitches are involved
- exact steps to reproduce the problem

Do not include your full license key. If a license issue needs investigation, include only the visible Machine ID and the exact error message.

## Privacy and Security

Audio routing, volume control, metering, spectrum analysis, and RT diagnostics run locally on your Mac.

License activation and validation use network requests for license status and seat management. VoluBridge may also check the update endpoint when you use the in-app update check.

## Uninstalling

Use `Remove App Completely` in VoluBridge when possible. It removes the app, driver, related settings, and Accessibility permission state.

Use `Remove Driver Only` if you want to keep the app and settings but remove `VoluBridgeRT.driver`.

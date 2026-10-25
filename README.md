<div align="center">

<img src="snap/gui/stirling-pdf.png" alt="Stirling-PDF logo" width="128" />

# Stirling-PDF

**PDF tools in your browser.**

[![stirling-pdf](https://snapcraft.io/stirling-pdf/badge.svg)](https://snapcraft.io/stirling-pdf)
[![Base: core26](https://img.shields.io/badge/Base-core26-2C8C3C?logo=canonical&logoColor=white)](https://snapcraft.io/core26)
![Confinement: strict](https://img.shields.io/badge/Confinement-strict-2C8C3C)
[![Maintainer: sidaliteir](https://img.shields.io/badge/Maintainer-sidaliteir-2C8C3C?logo=snapcraft&logoColor=white)](https://snapcraft.io/publisher/sidaliteir)
![Architectures: amd64 and arm64](https://img.shields.io/badge/Architectures-amd64%20%7C%20arm64-2C8C3C?logo=linux&logoColor=white)

[Getting Started](#getting-started) · [Configure](#configure) · [Limitations](#limitations) · [Build](#build) · [Support](#support) · [License](#license)

Unofficial snap packaging for [Stirling-PDF](https://github.com/Stirling-Tools/Stirling-PDF), a web application for working with PDF documents.

</div>

---

## Getting Started

<a href="https://snapcraft.io/stirling-pdf"><img alt="Get it from the Snap Store" src="https://snapcraft.io/en/dark/install.svg" width="180"></a>

```bash
sudo snap install stirling-pdf
```

The service starts automatically. Open [http://127.0.0.1:8080](http://127.0.0.1:8080).

This packages the Core edition without login. Use an authenticated HTTPS reverse proxy before exposing it outside your device.

## Configure

| Setting | Accepted values | Default |
| --- | --- | --- |
| `addr` | IP address or hostname | `127.0.0.1` |
| `port` | Integer `1`–`65535` | `8080` |

```bash
sudo snap get stirling-pdf
sudo snap set stirling-pdf port=9000
```

Changes restart the running service. Unsetting a setting restores its default. Set `addr=0.0.0.0` to listen on all interfaces.

Configuration, logs and data live in `/var/snap/stirling-pdf/common`. Edit `configs/custom_settings.yml` for application settings, then run `sudo snap restart stirling-pdf`.

English OCR is included. Add other language `.traineddata` files to `/var/snap/stirling-pdf/common/tessdata` and restart. For external watched folders:

```bash
sudo snap connect stirling-pdf:removable-media
```

Stop the service before backing up `/var/snap/stirling-pdf/common`.

## Limitations

- No accounts, SSO or AI features in this Core package.
- Tools requiring LibreOffice, Calibre, WeasyPrint, OCRmyPDF, ImageMagick or Python/OpenCV are unavailable.
- Browser uploads work normally. Server-side folders must be inside the snap's data directory or connected `/mnt` and `/media` mounts.
- `snap revert` restores the application, not its shared data or configuration.

## Build

```bash
git clone https://github.com/sidalit/stirling-pdf-snap.git
cd stirling-pdf-snap
sudo snap install snapcraft --classic
snapcraft pack
```

## Support

- **Installation or snap issues:** [open a packaging issue](https://github.com/sidalit/stirling-pdf-snap/issues).
- **Application bugs:** [report them upstream](https://github.com/Stirling-Tools/Stirling-PDF/issues).

## License

Snap packaging: [MIT](https://github.com/sidalit/stirling-pdf-snap/blob/main/LICENSE).

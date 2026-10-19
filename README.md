# Stirling-PDF snap

[![stirling-pdf](https://snapcraft.io/stirling-pdf/badge.svg)](https://snapcraft.io/stirling-pdf)

Snap packaging for [Stirling-PDF](https://github.com/Stirling-Tools/Stirling-PDF), a self-hosted toolbox for merging, splitting, converting and editing PDF documents.

Unofficial build, not affiliated with or endorsed by the Stirling-PDF project.

## Build

```bash
snapcraft pack
```

## Install and try

<a href="https://snapcraft.io/stirling-pdf"><img alt="Get it from the Snap Store" src="https://snapcraft.io/en/dark/install.svg" width="180"></a>

```bash
sudo snap install ./stirling-pdf_*.snap --dangerous
# After publication: sudo snap install stirling-pdf
```

The service starts right away and listens on `127.0.0.1:8080`. Open http://localhost:8080. This edition has no built-in login; use an authenticated HTTPS reverse proxy before opening it to other users.

## Background service

```bash
sudo snap logs stirling-pdf       # view logs
sudo snap restart stirling-pdf    # restart
sudo snap stop --disable stirling-pdf
sudo snap start --enable stirling-pdf
```

### Settings

`addr` defaults to `127.0.0.1` and `port` to `8080`. Changes restart a running service. Use `snap unset stirling-pdf <setting>` to restore its default.

```bash
sudo snap get stirling-pdf
sudo snap set stirling-pdf port=9000
sudo snap connect stirling-pdf:removable-media   # optional: /media, /mnt
```

Data, configuration and logs are in `/var/snap/stirling-pdf/common`. Advanced settings go in `configs/custom_settings.yml`; restart the service after editing it. Use `addr=0.0.0.0` only when access is protected.

## Known limitations

- No built-in login, accounts, SSO or AI features.
- LibreOffice, Calibre, WeasyPrint, OCRmyPDF, ImageMagick and Python/OpenCV are not included. Tools that need them are unavailable.
- OCR includes English. Add other Tesseract `.traineddata` files to `/var/snap/stirling-pdf/common/tessdata` and restart.
- Watched folders must be in the snap's data directory or connected external storage. Browser uploads work normally.
- `snap revert` restores the application, not its data. Stop the service before backing up `/var/snap/stirling-pdf/common`.

## Update to a new upstream release

Change `source-tag` in `snap/snapcraft.yaml`, then rebuild. The version is taken from the tag.

## Automation

Builds, publishing, and dependency updates use [snap-automation](https://github.com/sidalit/snap-automation).

## License

The packaging is MIT-licensed (see `LICENSE`). Stirling-PDF's core is MIT-licensed; its dependencies carry their own licenses.

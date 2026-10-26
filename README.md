# ONU Config Generator

A free, single-page web tool that generates ONU provisioning commands for GPON OLTs. Enter the ONU details, copy the commands, and paste them into the OLT CLI.

**Live site:** https://eleashs.github.io/OlT-Config-Vsol-And-C-Data/

## Supported OLTs

- VSOL GPON
- C-Data GPON

## How to use

1. Choose the OLT type (VSOL GPON or C-Data GPON).
2. **Single:** fill in Index, VLAN, SN and CID. For C-Data, also enter the PON.
3. **Batch:** add one row per ONU (or paste rows from Excel under "Paste from Excel"). Use **Add row** to continue with the next index.
4. Click **Copy commands** and paste them into the OLT CLI.
5. Use **Index finder** to paste the OLT's ONU list and find the next free index.

## Features

- Command templates for VSOL and C-Data GPON
- Single mode and Batch mode with one input row per ONU
- Excel paste import (tab, comma or space separated)
- One `write` / `save` at the end of a batch
- Warnings for empty fields, non-numeric index, and duplicate index or SN
- Index finder for the next free ONU index
- Editable command templates, saved in your browser
- One-click copy, works on phones and desktops, light and dark mode
- No backend and no login. Everything runs in your browser, and no data is sent anywhere.

## Notes

- The templates follow the commands used on our OLTs. CLI syntax can differ between OLT models and firmware, so test on one ONU before regular use.
- On VSOL, enter the correct PON interface in the CLI before pasting the commands.
- Inputs and edited templates are stored in the browser's local storage. Clearing browser data removes them, so keep a copy of your edited templates. Use **Clear all rows** when you finish on a shared device.

## Run locally

Download `index.html` and open it in a browser. For the copy button to work reliably, serve it over HTTPS (GitHub Pages) or localhost.

## Author

© 2026 Elias Hossen. All rights reserved.

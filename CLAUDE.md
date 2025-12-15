# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Thai Smartcard Reader is a React component library for reading Thai citizen smart cards. It requires the WebCard browser plugin and a physical smartcard reader device.

**Browser Support:** Safari 11, IE 9+, Firefox 51, Chrome 44 (newer versions of Firefox/Chrome not supported due to NPAPI deprecation)

## Build Commands

```bash
npm run build    # Build the library (webpack)
npm run start    # Watch mode for development
```

No test suite is configured.

## Architecture

This is a single-component React library published to npm. The entire implementation is in `src/index.js`.

**Key Components:**
- `ThaiSmartcardReader` - Main React component that embeds an invisible `<object>` element for the WebCard plugin
- Uses APDU commands to communicate with the smartcard via the WebCard browser plugin
- Outputs data through an `onChange` prop callback

**APDU Command Flow:**
1. Select applet: `00A4040008A000000054480001`
2. Read citizen ID, person info, address, issue/expiry dates, and photo image
3. Data is hex-encoded and converted via `hex2string()` which handles Thai character encoding (adds 3424 offset for Thai chars)

**Build Output:**
- Entry: `src/index.js`
- Output: `build/index.js` (commonjs2 format for npm consumption)
- React is externalized (uses consumer's React)

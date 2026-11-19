# WL Tag Uploader

A one-page phone uploader for Zhsunyco / WOLINK Bluetooth e-paper shelf tags (tested target: **BLE-35BWRY**, 3.5" black/white/red/yellow, 384 × 184).

**Use it:** https://richard-wals.github.io/wl-tag-uploader/ — open in **Chrome on Android** (Web Bluetooth needed).

1. Pick a picture and/or type up to three lines of text.
2. Check the preview.
3. Tap **Connect & send**, choose the tag (name starts with `WL`), wait for the refresh.

If the image shows upside down, tick **Rotate 180°**.

## How it works

Everything runs in the browser — no app, no server, no Home Assistant:

- Unlock: read the tag's nonce, answer with AES-128-ECB using the vendor key.
- Image: 2 bits per pixel (black 0, white 1, yellow 2, red 3), rotated into the panel's scan order.
- Upload: 8 KiB blocks of raw DEFLATE behind an `A5 A6` header, written in chunks with command `0xA500`, then refresh with `0xA502`.

Protocol details ported from [eigger/hass-ble-esl](https://github.com/eigger/hass-ble-esl) (MIT), preset `350`.

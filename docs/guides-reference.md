---
title: Guides & Reference
description: Disc ID related tools and guides
---


# Guides & Reference

## Guides
Hopefully these resources can help you try out some of the technologies the Disc ID Project will be using. Here are some fairly basic steps to get you started playing around with NFC tags:

1. Buy some NFC tags - many different types will work, but the popular NTAG ones are probably easiest to find. Stickers are nice so you can attach the tags to discs, these [NTAG 215](https://www.amazon.com/gp/product/B075CFXY8V) ones work well.
2. Download a free app that can read and write tags. Try NFC Tools on [iOS](https://apps.apple.com/us/app/nfc-tools/id1252962749) or [Android](https://play.google.com/store/apps/details?id=com.wakdev.wdnfc&hl=en_US&gl=US&pli=1).
3. Use the app to play around with adding and reading different records - especially the URL / URI record which allows for a record that matches the proposed [Record 1: NFC Forum Well-Known Type - URI](specifications/disc-id.md#record-1-nfc-forum-well-known-type-uri). Make sure you don't us the "Lock tag" option, as that permanently prevents writing the tag again.

--8<-- "help_out.md"

---

## Reference

### Python

[NDEF Decoder and Encoder for Python](https://ndeflib.readthedocs.io/en/stable/index.html){ target=_blank}

[Python module for near field communication](https://nfcpy.readthedocs.io/en/v0.13.6/index.html){ target=_blank}

### iOS

[Apple Core NFC Documentation](https://developer.apple.com/documentation/corenfc){ target=_blank}


### Android

[Android NFC Documentation](https://developer.android.com/reference/android/nfc/package-summary){ target=_blank}





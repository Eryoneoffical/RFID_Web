# ERYONE Filament RFID — Smart Tags for Your Spools 🎯



Ever wish your 3D printer just *knew* what filament you loaded? That's exactly what this project does. ERYONE's RFID protocol lets you store filament settings directly on a small NFC sticker attached to your spool. Tap it with your phone and instantly see the material type, color, print temperatures, and more — no app required.

It works with any NFC-enabled phone. 

**Why define a new protocol?**
- Any phone can read it — no special app needed, just a browser
- Human-readable text format, easy to understand and edit
- You can customize tags for your own use (e.g. label a spool as yours so others don't accidentally grab it)
- Easy to tag your own spools in bulk, even from other brands


![ERYONE RFID Demo](32.gif)


---


## How the Data is Stored

Each NFC tag holds a short text string that encodes all your filament's details. It's designed to be compact, readable, and safe to embed in a URL — so scanning the tag can open a webpage that displays everything nicely.

### Format at a Glance
- Starts with `en~`
- Ends with `~`
- Fields are separated by `-` (hyphens)

### Fields in Order

| # | Field | Description & Example |
|---|-------|-----------------------|
| 0 | URL | Always: `https://eryoneoffical.github.io/RFID_Web/?data=` |
| 1 | Header | Always: `en~` |
| 2 | Manufacturer | e.g. `ERYONE` |
| 3 | Material | e.g. `PLA`, `ABS`, `PETG` |
| 4 | Sub-type | Optional — leave blank if not needed |
| 5 | Color | Hex color code (6 digits) — e.g. `000000` = black, `FF0000` = red |
| 6 | Transparency | Hex opacity — `00` = clear, `FF` = solid |
| 7 | Min Print Temp | In °C — e.g. `190` |
| 8 | Max Print Temp | In °C — e.g. `230` |
| 9 | Bed Temp | In °C — e.g. `60` |
| 10 | Diameter | Stored ×100 — e.g. `175` means 1.75mm |
| 11 | Weight | In grams — e.g. `1000` |
| 12 | Production Date | `YYMM` format — e.g. `2602` = Feb 2026 |
| 13 | Tail | Always: `~` |

### Example

```
en~ERYONE-PLA--000000-FF-190-230-60-175-1000-2602~
```

Breaking that down:
- **Brand:** ERYONE
- **Material:** PLA (no sub-type)
- **Color:** Black (#000000), fully opaque
- **Print temp:** 190°C – 230°C
- **Bed temp:** 60°C
- **Diameter:** 1.75mm
- **Weight:** 1000g
- **Made:** February 2026

### Full URL (what gets written to the tag)

```
https://eryoneoffical.github.io/RFID_Web/?data=en~ERYONE-PLA--000000-FF-190-230-60-175-1000-2602~
```

Scan this with any phone and it opens a webpage showing all the filament details automatically.

---

## The Web Tool 🌐

**👉 https://eryoneoffical.github.io/RFID_Web/**

This is your one-stop tool for reading and writing filament tags. Open it in Chrome on Android and you can interact with NFC tags directly — no extra apps needed.

### What You Can Do

1. **Read a tag** — Tap "Start Reading", hold your phone near the tag, and the filament info pops up automatically.
2. **Write a tag** — Fill in your filament details using the form, then tap to write it to a blank NFC tag in one go.
3. **Share via link** — Any URL with `?data=...` will display the filament info right in the browser, even without an NFC tag involved.

### Android vs iPhone

| | Android | iPhone |
|---|---------|--------|
| Read tags | ✅ Chrome (built-in NFC) | ✅ Scan tag → opens webpage |
| Write tags | ✅ Chrome (built-in NFC) | ⚠️ Use a third-party NFC app with the generated data string |
| View via URL | ✅ | ✅ |

---

## Good to Know

- All characters used in the data format are URL-safe (letters, numbers, `-`, `~`), so no messy encoding is needed.
- Blank NFC stickers like the **NTAG213** work great for this.
- You can tag spools from any brand, not just ERYONE!

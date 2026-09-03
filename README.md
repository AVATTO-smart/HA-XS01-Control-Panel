# HA-XS01 Control Panel — Firmware

Firmware releases for the ESP32-P4 HA-XS01 control panel.

## Downloads

[GitHub Releases](https://github.com/AVATTO-smart/HA-XS01-Control-Panel/releases)

| File | Purpose |
|------|---------|
| `firmware.factory.bin` | Full image for USB flashing (write at offset `0x0`) |
| `firmware.bin` | OTA update package (Settings → Firmware → Upgrade) |

Do **not** flash `firmware.bin` at `0x0` — it is for OTA only.

## USB flash (`firmware.factory.bin`)

### One-time setup

Install [esptool](https://docs.espressif.com/projects/esptool/en/latest/esp32p4/) once (`pip install esptool`, or use the copy bundled with ESPHome / ESP-IDF).

If `esptool.py` is on your PATH (e.g. ESP-IDF shell), you can use it instead of `python -m esptool` — same commands, same result.

### Flash

1. Download **`firmware.factory.bin`** from Releases.
2. Connect the panel to your PC with USB Type-C and note the serial port (e.g. `COM5` on Windows, `/dev/ttyACM0` on Linux).
3. Close any serial monitor or other app using the COM port.
4. Run:

```bash
# Optional: erase entire flash
python -m esptool --chip esp32p4 -p COM5 erase-flash

# Write firmware.factory.bin from offset 0x0
python -m esptool --chip esp32p4 -p COM5 -b 460800 write-flash 0x0 firmware.factory.bin
```

5. Power-cycle the panel and follow the on-screen prompts.

## OTA update

On the panel, open **Settings → Firmware**. When a newer version is available, tap **Upgrade**.

# macOS (in progress)

Not tested yet. These steps follow the [official Kanata macOS docs](https://github.com/jtroo/kanata/blob/main/docs/setup-macos.md).

## 7.0 Gather information

```bash
sw_vers; uname -m
defaults read ~/Library/Preferences/com.apple.HIToolbox.plist AppleSelectedInputSources | grep -i "KeyboardLayout Name"
ls /Applications | grep -i karabiner || echo "no Karabiner"
systemextensionsctl list 2>/dev/null | grep -i karabiner || echo "no Karabiner driver"
```

The active keyboard layout determines what `config/macos/f75.kbd` will look like. Karabiner-Elements, if installed, competes with Kanata for the keyboard.

## 7.1 Driver

1. Install the **Karabiner-DriverKit-VirtualHIDDevice** `.pkg`, using the version listed in the Kanata release notes (v8.0.0 when this guide was written).
2. Activate it:
   ```bash
   sudo /Applications/.Karabiner-VirtualHIDDevice-Manager.app/Contents/MacOS/Karabiner-VirtualHIDDevice-Manager forceActivate
   ```
3. **System Settings → General → Login Items & Extensions → Driver Extensions:** enable `org.pqrs.Karabiner-DriverKit-VirtualHIDDevice`.

## 7.2 Kanata

```bash
sudo mv kanata-macos-arm64 /usr/local/bin/kanata   # x64 on Intel Macs
sudo chmod +x /usr/local/bin/kanata
/usr/local/bin/kanata --macos-request-permissions || true
```

Add `/usr/local/bin/kanata` under **Privacy & Security → Input Monitoring** and **Accessibility**.

## 7.3 Test

```bash
# Terminal 1
sudo "/Library/Application Support/org.pqrs/Karabiner-DriverKit-VirtualHIDDevice/Applications/Karabiner-VirtualHIDDevice-Daemon.app/Contents/MacOS/Karabiner-VirtualHIDDevice-Daemon"
# Terminal 2
sudo kanata -c ~/.config/kanata/f75.kbd
```

## 7.4 Start with macOS

To do: LaunchDaemons for the driver and for Kanata.

## Notes

- The F75 Win key becomes **Command** and Alt becomes **Option**. An optional Win ↔ Alt swap would put Command next to Space, like on an Apple keyboard.
- macOS has no AltGr, and its Brazilian layouts differ from the Windows/Linux ABNT2.

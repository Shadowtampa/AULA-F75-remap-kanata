# Windows

## Step 0: Preparation

1. In the AULA software, export a backup of your profile (export icon next to "Profile").
2. In **Settings → Time & language → Language & region**, make sure the keyboard is **Portuguese (Brazil ABNT2)**.

## Step 1: Swap Fn ↔ Right Ctrl in the AULA software

1. Open **Key assignment** and keep the **Default** tab selected.
2. Click the **Fn** key in the drawing and choose **RCtrl** (under Modify).
3. Click the **Ctrl** key to its right and choose **FN**.
4. Save (floppy disk icon).

Test: in Notepad, holding the key right of Space + A should select all.

## Step 2: Install Kanata

1. Create the folder `C:\Kanata`.
2. Download the Windows `.zip` from [github.com/jtroo/kanata/releases](https://github.com/jtroo/kanata/releases).
3. Copy into `C:\Kanata`:
   - the file with **tty + winIOv2 + x64** in its name, renamed to `kanata.exe` (console version, good for testing);
   - the file with **gui + winIOv2 + x64** in its name, renamed to `kanata_gui.exe` (system tray version, for daily use).
4. Copy [`config/windows/f75.kbd`](../../config/windows/f75.kbd) to `C:\Kanata\f75.kbd`.

Avoid the `wintercept` variant, which requires installing the Interception driver.

## Step 3: First run

In PowerShell:

```powershell
cd C:\Kanata
.\kanata.exe -c f75.kbd
```

Keep the window open. **Left Ctrl + Space + Esc** quits Kanata.

## Step 4: Test

Check the layer tables in the [README](../../README.en.md) using Notepad.

## Step 5: Start with Windows (system tray icon)

1. **Win + R** → `shell:startup` → Enter.
2. Right-click → **New → Shortcut**, with the target:
   ```
   C:\Kanata\kanata_gui.exe -c C:\Kanata\f75.kbd
   ```
3. Name it **Kanata** and finish.

Kanata now starts automatically, with no window and an icon in the system tray (it may be hidden under the **^** arrow). Right-click the icon to reload the config.

## Known issues

- **Cable not recognized:** check the mode switch on the back of the keyboard, push the cable all the way in and use a data cable (not charge-only). Kanata also works over the 2.4 GHz dongle.
- **Braces and brackets swapped:** the correct order in the config is `(fork (unshift ]) S-] ...)`. This was confirmed on the real keyboard, on both Windows and Linux.

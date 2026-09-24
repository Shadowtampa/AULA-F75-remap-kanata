# Linux (tested on Ubuntu 24.04, GNOME)

Kanata must run on the computer the F75 is connected to. Installation can be done over SSH.

## 6.1 OS keyboard layout

**Settings → Keyboard → Input Sources:** put **Portuguese (Brazil)** first.

## 6.2 Install Kanata

```bash
sudo apt install -y unzip curl
cd /tmp && rm -rf kanata_dl && mkdir kanata_dl && cd kanata_dl
URL=$(curl -s https://api.github.com/repos/jtroo/kanata/releases/latest | grep -o 'https://[^"]*linux[^"]*x64[^"]*\.zip' | head -1); echo "LINK: $URL"
curl -L -o kanata.zip "$URL" && unzip -o kanata.zip && ls -la
sudo install -m 755 /tmp/kanata_dl/kanata_linux_x64 /usr/local/bin/kanata
kanata --version
```

Use `kanata_linux_x64`, not the `cmd_allowed` build, which allows running shell commands from the keyboard.

Copy the config:

```bash
mkdir -p ~/.config/kanata
cp config/linux/f75.kbd ~/.config/kanata/f75.kbd
kanata --check -c ~/.config/kanata/f75.kbd
```

## 6.3 Permissions (no sudo needed afterwards)

```bash
sudo groupadd --system uinput
sudo usermod -aG input,uinput $USER
echo 'KERNEL=="uinput", MODE="0660", GROUP="uinput", OPTIONS+="static_node=uinput"' | sudo tee /etc/udev/rules.d/99-input.rules
echo uinput | sudo tee /etc/modules-load.d/uinput.conf
sudo reboot
```

After rebooting, `groups` should list `input` and `uinput`, and `ls -l /dev/uinput` should show `crw-rw---- root uinput`.

## 6.4 Test

```bash
kanata -c ~/.config/kanata/f75.kbd
```

Type on the F75 in a text editor and check the tables in the [README](../../README.en.md). Press **Ctrl+C** in the terminal (or `pkill kanata` over SSH) to stop.

## 6.5 Start on login

```bash
mkdir -p ~/.config/systemd/user
cp linux/kanata.service ~/.config/systemd/user/kanata.service
systemctl --user daemon-reload
systemctl --user enable --now kanata.service
systemctl --user status kanata.service --no-pager
```

The service starts at login with no window or icon. `loginctl enable-linger` would start Kanata before login, but it also starts every other user service early, so it was not used.

| To | Command |
|---|---|
| Reload after editing the config | `systemctl --user restart kanata` |
| Stop | `systemctl --user stop kanata` |
| View errors | `journalctl --user -u kanata -n 30 --no-pager` |
| Disable autostart | `systemctl --user disable kanata` |

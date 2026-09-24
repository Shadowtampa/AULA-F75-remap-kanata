# Linux (testado no Ubuntu 24.04, GNOME)

O Kanata precisa rodar no computador onde o F75 está conectado. A instalação pode ser feita por SSH.

## 6.1 Layout do sistema

**Configurações → Teclado → Fontes de entrada:** deixe **Português (Brasil)** em primeiro.

## 6.2 Instalar o Kanata

```bash
sudo apt install -y unzip curl
cd /tmp && rm -rf kanata_dl && mkdir kanata_dl && cd kanata_dl
URL=$(curl -s https://api.github.com/repos/jtroo/kanata/releases/latest | grep -o 'https://[^"]*linux[^"]*x64[^"]*\.zip' | head -1); echo "LINK: $URL"
curl -L -o kanata.zip "$URL" && unzip -o kanata.zip && ls -la
sudo install -m 755 /tmp/kanata_dl/kanata_linux_x64 /usr/local/bin/kanata
kanata --version
```

Use o `kanata_linux_x64` e não o `cmd_allowed`, que permite executar comandos pelo teclado.

Copie a configuração:

```bash
mkdir -p ~/.config/kanata
cp config/linux/f75.kbd ~/.config/kanata/f75.kbd
kanata --check -c ~/.config/kanata/f75.kbd
```

## 6.3 Permissões (sem sudo)

```bash
sudo groupadd --system uinput
sudo usermod -aG input,uinput $USER
echo 'KERNEL=="uinput", MODE="0660", GROUP="uinput", OPTIONS+="static_node=uinput"' | sudo tee /etc/udev/rules.d/99-input.rules
echo uinput | sudo tee /etc/modules-load.d/uinput.conf
sudo reboot
```

Depois de reiniciar, `groups` deve listar `input` e `uinput`, e `ls -l /dev/uinput` deve mostrar `crw-rw---- root uinput`.

## 6.4 Testar

```bash
kanata -c ~/.config/kanata/f75.kbd
```

Digite no F75 num editor de texto e confira as tabelas do [README](../README.md). **Ctrl+C** no terminal (ou `pkill kanata` pelo SSH) para parar.

## 6.5 Iniciar com o sistema

```bash
mkdir -p ~/.config/systemd/user
cp linux/kanata.service ~/.config/systemd/user/kanata.service
systemctl --user daemon-reload
systemctl --user enable --now kanata.service
systemctl --user status kanata.service --no-pager
```

O serviço inicia no login e não aparece janela nem ícone. `loginctl enable-linger` faria o Kanata iniciar antes do login, mas também antecipa todos os outros serviços de usuário, então não foi usado.

| Para | Comando |
|---|---|
| Recarregar após mudar o arquivo | `systemctl --user restart kanata` |
| Desligar | `systemctl --user stop kanata` |
| Ver erros | `journalctl --user -u kanata -n 30 --no-pager` |
| Parar de iniciar sozinho | `systemctl --user disable kanata` |

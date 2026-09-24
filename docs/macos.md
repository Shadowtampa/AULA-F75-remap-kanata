# macOS (em andamento)

Ainda não testado. Os passos seguem a [documentação oficial do Kanata para macOS](https://github.com/jtroo/kanata/blob/main/docs/setup-macos.md).

## 7.0 Levantar informações

```bash
sw_vers; uname -m
defaults read ~/Library/Preferences/com.apple.HIToolbox.plist AppleSelectedInputSources | grep -i "KeyboardLayout Name"
ls /Applications | grep -i karabiner || echo "sem Karabiner"
systemextensionsctl list 2>/dev/null | grep -i karabiner || echo "sem driver Karabiner"
```

O layout ativo decide como será o `config/macos/f75.kbd`. O Karabiner-Elements, se instalado, disputa o teclado com o Kanata.

## 7.1 Driver

1. Instale o `.pkg` do **Karabiner-DriverKit-VirtualHIDDevice** na versão pedida pelas notas da release do Kanata (v8.0.0 na época deste guia).
2. Ative:
   ```bash
   sudo /Applications/.Karabiner-VirtualHIDDevice-Manager.app/Contents/MacOS/Karabiner-VirtualHIDDevice-Manager forceActivate
   ```
3. **Ajustes do Sistema → Geral → Itens de Início e Extensões → Extensões de Driver:** ligue `org.pqrs.Karabiner-DriverKit-VirtualHIDDevice`.

## 7.2 Kanata

```bash
sudo mv kanata-macos-arm64 /usr/local/bin/kanata   # x64 em Mac Intel
sudo chmod +x /usr/local/bin/kanata
/usr/local/bin/kanata --macos-request-permissions || true
```

Adicione `/usr/local/bin/kanata` em **Privacidade e Segurança → Monitoramento de Entrada** e **Acessibilidade**.

## 7.3 Testar

```bash
# Terminal 1
sudo "/Library/Application Support/org.pqrs/Karabiner-DriverKit-VirtualHIDDevice/Applications/Karabiner-VirtualHIDDevice-Daemon.app/Contents/MacOS/Karabiner-VirtualHIDDevice-Daemon"
# Terminal 2
sudo kanata -c ~/.config/kanata/f75.kbd
```

## 7.4 Iniciar com o macOS

A fazer: LaunchDaemons para o driver e para o Kanata.

## Observações

- A tecla Win do F75 vira **Command** e o Alt vira **Option**. Uma troca opcional Win ↔ Alt deixaria o Command ao lado do Espaço, como num teclado Apple.
- O macOS não tem AltGr, e os layouts brasileiros dele diferem do ABNT2 do Windows/Linux.

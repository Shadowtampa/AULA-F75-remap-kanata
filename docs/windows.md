# Windows

## Etapa 0: Preparação

1. No software da AULA, exporte um backup do seu perfil (ícone de exportar ao lado de "Profile").
2. Em **Configurações → Hora e idioma → Idioma e região**, confira se o teclado está como **Português (Brasil ABNT2)**.

## Etapa 1: Trocar Fn ↔ Ctrl direito no software da AULA

1. Abra **Key assignment** e deixe a aba **Default** selecionada.
2. Clique na tecla **Fn** do desenho e escolha **RCtrl** (em Modify).
3. Clique na tecla **Ctrl** à direita dela e escolha **FN**.
4. Salve (ícone de disquete).

Teste: no Bloco de Notas, segurar a tecla ao lado do Espaço + A deve selecionar tudo.

## Etapa 2: Instalar o Kanata

1. Crie a pasta `C:\Kanata`.
2. Baixe o `.zip` para Windows em [github.com/jtroo/kanata/releases](https://github.com/jtroo/kanata/releases).
3. Copie para `C:\Kanata`:
   - o arquivo com **tty + winIOv2 + x64** no nome, renomeado para `kanata.exe` (versão com janela, boa para testar);
   - o arquivo com **gui + winIOv2 + x64** no nome, renomeado para `kanata_gui.exe` (versão com ícone na bandeja, para o dia a dia).
4. Copie [`config/windows/f75.kbd`](../config/windows/f75.kbd) para `C:\Kanata\f75.kbd`.

Evite a variante `wintercept`, que exige instalar o driver Interception.

## Etapa 3: Primeira execução

No PowerShell:

```powershell
cd C:\Kanata
.\kanata.exe -c f75.kbd
```

A janela precisa ficar aberta. **Ctrl esquerdo + Espaço + Esc** fecha o Kanata.

## Etapa 4: Testar

Confira as tabelas de camadas do [README](../README.md) no Bloco de Notas.

## Etapa 5: Iniciar com o Windows (ícone na bandeja)

1. **Win + R** → `shell:startup` → Enter.
2. Botão direito → **Novo → Atalho**, com o destino:
   ```
   C:\Kanata\kanata_gui.exe -c C:\Kanata\f75.kbd
   ```
3. Dê o nome **Kanata** e conclua.

O Kanata passa a abrir sozinho, sem janela, com um ícone na bandeja (pode estar escondido na setinha **^**). Clique com o botão direito no ícone para recarregar a configuração.

## Problemas conhecidos

- **Cabo não reconhecido:** confira a chave de modo atrás do teclado, empurre o cabo até o fim e use um cabo que transfira dados (não só carregue). O Kanata funciona também pelo dongle 2.4 GHz.
- **Chaves e colchetes invertidos:** a ordem correta na configuração é `(fork (unshift ]) S-] ...)`. Isso foi confirmado no teclado real, no Windows e no Linux.

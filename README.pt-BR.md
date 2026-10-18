# NSPackBuilder

[English](README.md) · [Português (Brasil)](README.pt-BR.md)

O **NSPackBuilder** é uma aplicação desktop para Windows destinada à montagem, manutenção e implantação de pacotes homebrew/CFW para Nintendo Switch. O programa baixa os componentes selecionados, cria um pacote local e pode copiá-lo para um cartão SD ou enviá-lo ao Switch por FTP.

> [!WARNING]
> O programa pode formatar unidades, apagar dados de cartões SD, gravar diretamente em dispositivos NAND físicos e injetar payloads. Essas operações podem causar perda irreversível de dados ou inutilizar o dispositivo quando executadas incorretamente. Sempre confirme a unidade selecionada, mantenha backups independentes e utilize somente hardware e arquivos autorizados.

## Principais recursos

- Seleção de pacotes, sysmodules, homebrews e arquivos de configuração.
- Download de assets de releases a partir dos repositórios configurados.
- Exibição de versões e contagens de downloads quando disponíveis.
- Criação de um pacote local com progresso e informações de tamanho.
- Cópia do pacote para uma unidade selecionada, preservando pastas configuradas.
- Formatação FAT32 e limpeza controlada de cartões SD.
- Criação e restauração de imagens de cartões SD.
- Inclusão de bootlogo usando os scripts Python integrados.
- Envio do pacote final para um servidor FTP compatível.
- Detecção de Switch em modo RCM e injeção de payloads.
- Backup e restauração de partições NAND através do Hekate.
- Dump de keys por FTP e migração de emuNAND entre conjuntos de keys.

## Conteúdo dos pacotes

A área **Packages** oferece distribuições configuradas como Kefir, Ultra, CNX, GNX e HATS.

A área **Sysmodules** oferece módulos e overlays como Tesla Menu, Ultrahand Overlay, sys-clk, MissionControl, SaltyNX, NX-ovlloader, Sys-FTPD e Status Monitor.

A área **Homebrew and files** oferece aplicações e arquivos de suporte como DBI, Goldleaf, Hekate Toolbox, Linkalho, NX Activity Log, NX Dump Tool, NX Gallery, instaladores de temas, hosts, Hekate IPL, boot files, patches e arquivos de configuração.

Os itens e versões disponíveis dependem dos repositórios configurados e podem mudar com o tempo.

## Fluxo de uso

1. Selecione os componentes desejados.
2. Escolha uma pasta de trabalho local.
3. Ative **Release Versions** para consultar metadados atuais das releases.
4. Clique em **Start** para baixar os arquivos e montar o pacote.
5. Use **Open Pack Folder**, **Copy Pack to Drive** ou **Send over FTP** conforme necessário.
6. Verifique o pacote gerado antes de utilizá-lo no console.

**Repo** baixa as releases mais recentes dos itens selecionados sem executar todo o fluxo do cartão SD. **Stop** interrompe um download ativo e **Restart** reinicia o estado atual.

## Operações no cartão SD

- **Format now**: formata a unidade selecionada em FAT32 e apaga todos os dados.
- **Create Image**: cria um arquivo de imagem a partir da unidade.
- **Restore Image**: grava uma imagem na unidade selecionada.
- Atualização da lista de unidades e ejeção segura.

As opções **Format SDCard** e **Erase SDcard / Keep emuMMC** são diferentes. A primeira usa a API de formatação do Windows; a segunda remove os dados do pacote permitindo preservar pastas configuradas, como emuMMC, Nintendo, atmosphere\\contents, DBISaves, bootloader\\nyx.ini e temas.

Confirme sempre a letra da unidade. Letras de unidades removíveis podem mudar quando cartões ou leitores são conectados e desconectados.

## Bootlogos e payloads

A página **Bootlogo** adiciona um bootlogo aos arquivos do firmware selecionado utilizando o runtime Python e os scripts incluídos.

A página **Boot / Payload** monitora o USB em busca de um Switch em modo RCM, lista payloads `.bin` presentes na pasta `payloads` e utiliza `TegraRcmSmash.exe` para injetar o payload escolhido.

## NAND e emuNAND

As ferramentas avançadas permitem:

- Fazer backup de partições NAND com progresso, velocidade e previsão de término.
- Restaurar uma partição a partir de um backup após confirmação explícita.
- Validar backups e exibir as partições detectadas.
- Injetar Hekate e aguardar a disponibilização do dispositivo NAND no Windows.
- Obter keys com `Lockpick_RCM_Pro` e salvá-las como `prod.keys`/`title.keys`.
- Converter uma emuNAND usando conjuntos de keys antigos e novos.

Essas operações exigem os arquivos adequados do Hekate, Lockpick e TegraRcmSmash, uma configuração compatível e, para acesso ao NAND físico, privilégios elevados no Windows. Leia o manual incluído antes de utilizá-las.

## FTP

O diálogo FTP oferece conexão anônima ou autenticada, host/porta configuráveis, navegação de diretórios, decisões de sobrescrever/pular arquivos e upload recursivo do pacote. As preferências são salvas em `SendFTP.ini`, ao lado do executável. Trate esse arquivo como sensível caso contenha credenciais.

## Requisitos

- Windows 10 ou posterior recomendado.
- Build Win32 do NSPackBuilder e seus arquivos complementares.
- Internet para downloads dos repositórios.
- Pasta local com espaço livre suficiente.
- Privilégios de administrador para formatação, acesso a discos físicos e algumas operações NAND.
- Leitor de cartão SD compatível.
- Payloads e executáveis auxiliares necessários às funções RCM/NAND.

Mantenha a estrutura de pastas ao mover o executável. As pastas `Win32\\Debug` e `Win32\\Release` contêm arquivos auxiliares como `TegraRcmSmash.exe`, `fat32format.exe`, payloads, DLLs e o runtime Python.

## Documentação incluída

- [Manual em português](docs/NSPackBuilder_OGuiaDeUso_PtBr.pdf)
- [Manual em inglês](docs/NSPackBuilder_UserGuide_En.pdf)

O próprio programa também pode extrair e abrir os manuais através da opção **Manual**.

## Compilação

O NSPackBuilder é uma aplicação Delphi VCL. Abra `NSPackBuilder.dproj` no RAD Studio, selecione a plataforma **Win32**, configure as dependências Delphi/DevExpress e compile a configuração **Release**.

O executável incorpora alguns recursos, mas outros arquivos permanecem externos. Uma compilação bem-sucedida não gera sozinha uma distribuição portátil completa.

## Estrutura do projeto

| Caminho | Finalidade |
| --- | --- |
| `sources/` | Forms Delphi, interface e lógica da aplicação |
| `resources/` | Arquivos compactados e recursos incorporados |
| `Python/` | Runtime Python e scripts de bootlogo |
| `docs/` | Manuais e imagens |
| `image/`, `icons/` | Artes e ícones |
| `Win32/Debug/`, `Win32/Release/` | Saídas de build e arquivos de distribuição |
| `Dcu/` | Units compiladas do Delphi |

## Créditos e suporte

O NSPackBuilder reúne arquivos e assets de vários projetos open source independentes. As licenças e condições de uso de cada componente continuam aplicáveis.

Para sugestões, problemas ou feedback, acesse o [repositório no GitHub](https://github.com/OneEyeBlack/NSPackBuilder).

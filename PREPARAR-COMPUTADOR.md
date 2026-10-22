# Preparar o computador da loja

Instruções para o **Claude Code** rodando no computador novo da loja Malenas Styles. O trabalho é instalar e deixar
pronto o **Malenas Gestão**, o sistema de caixa da loja. Fale com a pessoa em português simples, um passo de cada vez,
e peça confirmação antes de qualquer coisa difícil de desfazer.

## Regras

- Os dados **reais** da loja ficam em `%LOCALAPPDATA%\PDV-Carol` e o sistema roda em `http://127.0.0.1:3210`.
  Nunca crie vendas, produtos, clientes ou contas de teste ali, nem rode testes contra essa porta.
  Para conferir, só leitura: `GET http://127.0.0.1:3210/api/auth/estado`.
- Aqui vai só o aplicativo: não instale Node nem Git, não baixe o código e não faça login no GitHub.
- A conta da dona (primeiro acesso, com o código de segurança no celular dela) é criada **pela própria dona** na
  tela do sistema. Não crie por ela.
- Nunca peça para digitarem senhas no chat. Logins (OneDrive, Tailscale, Windows) a pessoa faz na tela.

## Passo a passo

1. **Conferir o computador:** Windows 11 (`winver`), 8 GB de memória ou mais, SSD. Windows Update em dia,
   Microsoft Defender ligado, data, hora e fuso (Brasília) certos.
2. **Energia:** com o computador na tomada, ele nunca pode suspender nem hibernar (os celulares perdem o acesso):
   `powercfg /change standby-timeout-ac 0` e `powercfg /change hibernate-timeout-ac 0`. A tela pode apagar.
   Explique que muitos computadores ligam sozinhos quando a luz volta, por uma opção da BIOS ("Restore on AC Power
   Loss" ou "After Power Loss" → Power On, tecla Del ou F2 ao ligar). Quem ajusta é a pessoa, na tela da BIOS.
3. **Rede:** a rede da loja deve estar como **Privada** (`Get-NetConnectionProfile`), senão o Windows bloqueia o
   acesso dos celulares pelo Wi-Fi. Pergunte antes de mudar. Se alguém tiver a senha do roteador, sugira reservar o
   IP deste computador: o acesso pelo Wi-Fi usa o número (ex.: 192.168.0.15) e, se ele mudar, os celulares leem o
   QR code de novo. Sem a senha, pule.
4. **Instalar:** baixe o `Malenas-Gestao-Setup-<versão>.exe` da versão mais recente em
   https://github.com/malenasgestao-cloud/malenas-gestao-atualizacoes/releases/latest e rode com `/S`.
   Confira que a porta 3210 responde e que existe
   `%LOCALAPPDATA%\Programs\malenas-gestao\resources\app-update.yml` (é o que faz as atualizações chegarem sozinhas).
5. **Impressora Bematech MP-4200 TH (USB):** confira que aparece como porta COM
   (`Get-CimInstance Win32_PnPEntity | Where-Object Name -match 'COM'`). O sistema acha sozinho; o teste de
   impressão a dona faz no sistema (Configurações → Impressora).
6. **OneDrive (backup):** a pessoa entra no OneDrive com a conta da loja (ícone de nuvem perto do relógio).
   Depois de fechar e abrir o sistema, confira que apareceu a pasta `OneDrive\Backup Malenas` com uma cópia `pdv-*.db`.
7. **Tailscale (dona acessar de qualquer lugar):** instale (https://tailscale.com/download/windows), rode
   `tailscale login` e passe o link para a pessoa aprovar com a conta da loja. Depois rode
   `tailscale set --unattended`, para ele conectar mesmo antes de alguém entrar no Windows.
8. **Voltar sozinho depois de desligar (pergunte antes):** o sistema só abre depois que alguém entra no Windows.
   Depois de uma queda de luz ou de uma atualização do Windows, o computador fica parado na tela do PIN e os celulares
   ficam sem acesso até alguém digitar. Explique e pergunte se o Windows deve entrar sozinho ao ligar. O Malenas
   Gestão continua pedindo usuário e senha; só o Windows passa a entrar direto. Se a pessoa quiser, use o Autologon
   da Microsoft (https://learn.microsoft.com/sysinternals/downloads/autologon). Ela digita a senha do Windows na
   janela dele, nunca no chat. Com conta Microsoft que só entra com PIN, desligue antes, em Configurações → Contas →
   Opções de entrada, a opção "permitir apenas a entrada do Windows Hello".
9. **Primeiro acesso (com a dona):** ela cria a conta, ativa o código de segurança no celular e anota os códigos de
   recuperação. Depois segue a lista **Primeiros passos** da tela inicial: dados da loja (já vêm preenchidos, só
   conferir e salvar), teste da impressora, produtos ("Importar do site"), estoque, backup, abrir com o Windows,
   funcionárias (a ficha de acesso imprime na Bematech) e celular (Wi-Fi e Tailscale, em Configurações → Aplicativo
   e celular). Se o Windows perguntar do firewall, **Permitir**.
10. **Conferência final:** impressora pronta; backup de hoje no OneDrive; um celular no Wi-Fi da loja abre o
    sistema; a dona entra pelo celular via Tailscale. Por último, reinicie o computador e, sem tocar em nada (ou só
    digitando o PIN, se não quiseram o passo 8), confira que o sistema abre sozinho e o celular volta a entrar.
11. **Ao terminar:** a pessoa sai da conta do Claude neste computador (ou desinstala o Claude Code). O computador
    fica na loja com dados de clientes.

## Se a loja já usava outro computador

Não comece do zero: no computador novo, entre no OneDrive da loja e espere a pasta `Backup Malenas` aparecer.
Instale (passo 4), faça o primeiro acesso com uma conta qualquer e vá em **Configurações → Backup → Restaurar** na
cópia mais recente: volta tudo (produtos, vendas, clientes, usuários e senhas). Depois, ligue de novo "abrir com o
Windows" e o acesso pelo celular (os celulares leem o QR code novo). O computador antigo não deve mais vender.

O menu **Ajuda** do sistema tem o passo a passo de tudo para o dia a dia.

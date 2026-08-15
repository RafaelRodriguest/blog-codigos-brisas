---
layout: post
title: 'Update: Omarchy Quattro'
author: cotes
date: 2026-08-15 11:00:00 -0300
categories: [Setup, Linux]
tags: [omarchy, hyprland, quickshell, linux, ia]
---

Alguns meses atrás escrevi aqui sobre minhas primeiras impressões com o Omarchy, quando ainda estava na versão 2.0 e eu migrava de vez pro Arch depois de anos pulando entre Ubuntu, Mint e WSL2. Na época o sistema já me convenceu pela produtividade imediata e pela estética limpa, mesmo com as peculiaridades de sempre do Linux moderno.

No dia 14 de agosto de 2026 o DHH lançou o **Omarchy Quattro (4.0)**, e ele próprio classificou como um dos maiores lançamentos de software da carreira dele. Então hoje, dia 15, resolvi fazer o update para testar.

> ![Meu desktop rodando o Omarchy Quattro](/assets/img/update-omarchy-quattro/screenshot-2026-08-15_10-45-23.webp)

Até o lançamento, o sistema passou por Alphas em julho e uma última *Release Candidate* na véspera, e a versão estável saiu tanto como atualização do sistema quanto como ISO nova direto no [GitHub do projeto](https://github.com/basecamp/omarchy/releases). No mesmo dia o DHH publicou um vídeo oficial e bem completo apresentando tudo.

{% include embed/youtube.html id='F7fe9pa8OeE' %}

Duas mudanças concentram o peso dessa versão: a interface do desktop foi reescrita do zero, e agentes de IA passaram a viver dentro do sistema operacional. Vou destrinchar cada uma.

## **O fim da colcha de retalhos**

Se você usou o Omarchy antes, sabe que a interface era, na prática, uma colcha de retalhos. A barra vinha do Waybar, as notificações do Mako, o launcher do Walker, os OSDs do SwayOSD, a tela de bloqueio do hyprlock, e por aí ia. Cada peça era um software independente, com sua própria configuração, e essa era exatamente a parte que mais quebrava a cada atualização do Arch.

No Quattro tudo isso foi jogado fora. A casca inteira do desktop foi reescrita usando **Quickshell**, um toolkit baseado em Qt Quick, e agora a barra, o launcher, os menus, as notificações, o bloqueio de tela e os alertas em tela rodam dentro de um único processo contínuo. Waybar, Walker, Mako, SwayOSD, hyprlock, hypridle, swaybg e polkit-gnome foram eliminados de vez.

A ISO ficou cerca de 1 GB menor e a instalação ficou uns 30% mais rápida. Mas o ganho real está na coesão: em vez de sincronizar cinco ou seis ferramentas que frequentemente brigavam entre si, você passa a ter uma casca única, totalmente tematizável e scriptável via IPC. Foi a primeira coisa que senti ao atualizar.

## **A IA deixou de ser aplicativo e virou sistema**

Aqui mora a mudança mais marcante, e também a mais polêmica. A maioria das distros trata IA como um aplicativo que você instala por fora. O Quattro faz o oposto: as ferramentas agênticas vêm embutidas no núcleo do sistema.

O exemplo que melhor traduz a ideia é o **Crash Watcher**. Ele se conecta ao `systemd-coredump` e, sempre que um processo quebra, o sistema resume o erro e oferece mandar o backtrace pro seu agente de IA padrão, através de uma skill chamada `diagnose-crash`, pra você receber um diagnóstico na hora. Em vez de caçar o log manualmente, o crash chega até você já mastigado.

Na primeira inicialização você escolhe o agente padrão em `Setup › Defaults › Agent`, entre nove opções, incluindo Claude Code, Codex, Gemini, Grok, Copilot, OpenCode, Pi e Oh My Pi. Junto vem um widget na barra que monitora os limites semanais de uso desses modelos, o que é uma sacada boa pra não tomar susto no fim do mês, e alguns aliases já prontos no shell, como `c` pro OpenCode e `cx` pro Claude Code em *danger mode*.

E aqui vem o detalhe importante de entender: é tudo opcional. Se você não escolher nenhum agente no primeiro boot, todas as funcionalidades agênticas simplesmente ficam desligadas. O DHH cravou uma direção forte, mas não empurrou ela goela abaixo, e isso respeita a filosofia "omakase" de sempre: o caminho vem pavimentado, mas você continua livre pra sair dele.

## **Plugins de verdade e o Hyprland em Lua**

Outra novidade que muda o dia a dia é o sistema de plugins. Agora dá pra instalar extensões com um comando direto, `omarchy plugin add <URL-do-repositório>`, e elas ficam desativadas por padrão até você ligar com `omarchy plugin enable <id>` ou pela interface em `Setup › Plugins`. Antes mesmo do lançamento final já havia mais de cem plugins no repositório da comunidade, o que mostra que o ecossistema não é mais só o DHH decidindo tudo sozinho.

A mudança maior é que o Hyprland abandonou o velho formato `.conf` e passou a usar **Lua** na configuração. Quem, como eu, customizou pesado seus atalhos e scripts no Omarchy anterior precisa ficar atento: o sistema tenta converter as configurações antigas automaticamente, e os próprios agentes de IA ajudam nessa migração, mas *bindings* muito complexos podem falhar e exigir ajuste manual, deixando marcações de `TODO` pra você resolver depois.

Vale lembrar que na minha experiência anterior foi justamente o `hyprland.conf` que eu mais mexi pra acertar meu segundo monitor. Então essa transição pro Lua é a parte que vou revisar com calma antes de confiar cegamente na conversão automática.

## **O que ainda melhorou**

Fora as duas grandes reescritas, o Quattro trouxe um monte de refinamento que resolve dores antigas. O que mais me interessa é o suporte a *dual boot*: antes o instalador exigia o disco inteiro, e agora dá pra instalar numa única partição, convivendo com Windows ou outra distro, sem abrir mão da criptografia LUKS por padrão. Isso derruba um dos obstáculos que eu mesmo apontei no post anterior.

O resto vem na mesma linha de polimento. O painel de rede foi reconstruído sobre o NetworkManager e integrado à interface do Quickshell, há um controle nativo do Tailscale pra alternar conexões e copiar IPs, o menu de aplicativos e as tarefas administrativas foram unificados num único menu pesquisável, e o anotador de capturas de tela ganhou marcações, setas e textos antes de salvar.

## **Como atualizar**

Se você já roda o Omarchy, dá pra migrar de duas formas. Pela interface, que é o caminho recomendado, é só pressionar `SUPER + ALT + SPACE` e ir em `Update › Omarchy › Update to Quattro`. Se preferir o terminal, ou se a interface der alguma instabilidade, o utilitário nativo resolve:

```bash
omarchy update
```

Eu fui pela atualização direta hoje mesmo, dia 15, pra sentir as mudanças na prática. E a impressão que ficou é a de um projeto amadurecendo na direção certa. Consolidar tudo no Quickshell é a decisão mais sensata que o Omarchy podia tomar: em vez de usar várias ferramentas que viviam brigando entre si, o sistema virou uma peça só, coesa e previsível. A aposta agressiva em IA vai dividir opiniões, mas o fato de tudo ser opcional mostra que o DHH entendeu onde traçar a linha.

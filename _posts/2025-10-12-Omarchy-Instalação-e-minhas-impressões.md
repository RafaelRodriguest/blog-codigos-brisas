---
layout: post
title: "Omarchy 2.0 : Minhas impressões"
author: cotes
date: 2025-10-12 10:00:00 -0300
categories: [Setup, Linux]
tags: [Linux, Omarchy,Setup,Minimalismo]
---

## **O Omarchy e sua filosofia**

O Omarchy é uma configuração de ambiente de desktop para o sistema operacional Linux, criada por David Heinemeier Hansson (DHH), o criador do framework Ruby on Rails e cofundador da empresa 37signals.
Ele não é uma distribuição Linux totalmente nova, mas sim uma instalação opinativa baseada no Arch Linux, que utiliza o gerenciador de janelas em mosaico Hyprland.

![Omarchy](/assets/img/omarchy1.png)
### **História**

O Omarchy evoluiu de um projeto anterior de DHH chamado Omakub, que era um conjunto de scripts para personalizar o Ubuntu para desenvolvimento no qual usei bastante quando utilizava o Ubuntu o que facilitava muito, pois vinha com muitas ferramentas de desenvolvimento pré-instaladas.

Com a crescente insatisfação de DHH com o macOS, ele passou a explorar o Linux e se impressionou com a experiência oferecida pelo Arch Linux e pelo Hyprland. O resultado dessa experimentação foi o Omarchy, que busca oferecer uma alternativa polida e moderna aos sistemas operacionais comerciais.

Eu passei por algumas distros Linux nos últimos anos como Ubuntu, Mint e, por último, usei bastante o WSL2 com a virtualização do Ubuntu visto que muitas ferramentas do trabalho eram compatíveis com o Windows 11, e eu precisava do Linux para desenvolvimento. Por isso, optei pelo WSL.

Porém, sempre ouvi falar da maturidade e filosofia do Arch Linux, principalmente por ser considerado difícil de instalar e configurar. Testei com uma instalação em máquina virtual do Manjaro, em ambiente GNOME, e tive a primeira sensação do quão penoso é ter que configurar tudo na mão. Ao mesmo tempo, é um excelente aprendizado, pois você se sente no controle de tudo e pode configurar o sistema do seu jeito, aprendendo mais sobre sistemas operacionais à medida que os bugs aparecem.

Além disso, o Arch Linux possui uma comunidade fantástica e o ArchWiki, que é praticamente uma bíblia: se você tiver alguma dúvida ou problema no Arch, provavelmente a solução estará lá.

Fiquei com aquele gostinho de querer usar no meu setup principal. Foi então que, em 2025, foi lançada a versão 2.0 do Omarchy, que passou de um conjunto de scripts de pós instalação para uma ISO completa, com repositório de pacotes e uma comunidade crescente de entusiastas.

O Omarchy vem com o Hyprland, que é um gerenciador de janelas focado em organizar janelas automaticamente em um layout de mosaico (“tiling”) sem sobreposição. Foi a minha primeira experiência usando esse tipo de sistema, o que me agradou bastante, pois consigo abrir várias telas nesse formato e trabalhar em tarefas paralelas ao mesmo tempo ou até mesmo abrir terminais de forma rápida, sem precisar usar um segundo monitor, aumentando a produtividade.

![Omarchy](/assets/img/omarchy-hyprland.png)


No Omarchy, o Hyprland vem todo pré-configurado, o que facilita bastante. E, se você quiser fazer alguma alteração, há o arquivo `~/.config/hypr/hyprland.conf`, onde é possível personalizar suas configurações de acordo com suas necessidades. Depois, é só dar o comando `hyprctl reload` para recarregar as configurações realizadas. Tive que fazer algumas modificações nesse arquivo para adaptar configurações do meu segundo monitor.

### **Filosofia**

A filosofia do Omarchy é centrada em alguns pilares principais:

#### **Opinativo (Opinionated)**

O Omarchy não busca ser uma tela em branco para o usuário configurar do zero. Em vez disso, ele oferece um conjunto de configurações e ferramentas pré-selecionadas por DHH, que ele considera ideais para uma experiência de desenvolvimento moderna e produtiva.
O objetivo é reduzir a “anarquia” de escolhas infinitas, oferecendo um caminho pavimentado (“omakase”, que significa “escolha do chef”, em japonês).
Muita gente gosta, e muita gente não gosta das escolhas de DHH é daí que vem a beleza do Linux: você pode mudar e colocar do seu jeito.

#### **Minimalista e orientado ao teclado**

O design é focado na produtividade e na velocidade, priorizando o uso do teclado em vez do mouse. A interface é limpa, sem ícones na área de trabalho ou dock, e todas as ações como abrir programas, alternar janelas e gerenciar o sistema  são todos controladas por atalhos de teclado.
Essa será uma das principais mudanças para quem não é acostumado a navegar apenas com o teclado. No começo causa estranheza, mas, pelo menos para mim, trouxe velocidade e produtividade para abrir e fechar ambientes de trabalho.

Por exemplo:

*   `Super + Enter` abre o terminal.
*   `Super + B` abre o Chromium.
*   `Super + W` fecha a janela selecionada.

DHH preparou um manual muito bem detalhado, com aquele formato minimalista que é a cara dele, onde você encontra isso e muito mais sobre o Omarchy: [https://learn.omacom.io/2/the-omarchy-manual](https://learn.omacom.io/2/the-omarchy-manual)

#### **Estética e produtividade**

A filosofia de DHH é que “um sistema bonito é um sistema motivador”, o que vai de encontro ao que ele evangeliza no Ruby on Rails e em seus keynotes mundo afora.
O Omarchy traz consigo uma estética visual polida, utilizando temas e configurações que o diferenciam de outros sistemas e o tornam agradável de usar.

### **Instalação**

Para instalar o Omarchy, existe um método principal simplificado e opções mais avançadas para usuários experientes.
O processo, que antes era uma série de scripts para personalizar uma instalação existente do Arch, evoluiu recentemente para uma instalação por meio de uma ISO dedicada, especialmente a partir da versão 2.0.

Para você que é da área de Ciência da Computação, programador ou deseja subir o nível em tecnologia, recomendo fortemente instalar e usar o Arch Linux do zero, configurando particionamentos, placas de rede e entendendo mais “por debaixo dos panos” de uma distro Linux.
Depois de dominar, pode optar pelo `archinstall`, onde basta digitar o comando `archinstall` e seguir o passo a passo.

Existem duas maneiras principais de instalar o Omarchy:

#### **1. Instalação simplificada via ISO (recomendado)**

*  Baixe a ISO no site oficial e grave-a em um pendrive usando o balenaEtcher (ou Rufus no Windows).
*  Dê boot pelo pendrive e siga o instalador guiado. O processo é rápido, levando entre 2 e 5 minutos, dependendo da velocidade do computador.
*  O instalador faz a maior parte do trabalho, incluindo o particionamento do disco (com criptografia total obrigatória) e a instalação do ambiente de desktop completo e das ferramentas opinativas.

#### **2. Instalação manual (avançado)**

* Comece com a ISO padrão do Arch Linux, faça a instalação manual (ou use o `archinstall`) e depois execute o script fornecido pelo Omarchy para configurar o ambiente e instalar os pacotes.



Uma coisa interessante são os temas que já vêm pré-instalados, que podem ser visualizados com as teclas `SUPER + CTRL + SHIFT + ESPAÇO`.
Porém, instalei outros temas bem bonitos disponíveis em: [https://github.com/topics/omarchy-theme](https://github.com/topics/omarchy-theme)

![Omarchy](/assets/img/omarchy-tokyo-night.png)

![Omarchy](/assets/img/omarchy-osaka-jade.jpg)

![Omarchy](/assets/img/omarchy-theme1.png)

![Omarchy](/assets/img/omarchy-theme2.png)

![Omarchy](/assets/img/omarchy-theme3.png)


Na prática, a primeira impressão não desaponta. A produtividade é imediata, graças a um setup pré-configurado e centrado no teclado que elimina distrações, e a fluidez do Hyprland garante uma experiência rápida e visualmente agradável. Para quem, como eu, estava cansado de gastar tempo ajustando o ambiente de trabalho, o Omarchy é uma verdadeira alavanca de produtividade. O ambiente de desenvolvimento, completo com ferramentas como Neovim e Mise, é consistente e torna a gestão de projetos mais simples, e a estética limpa do sistema ajuda a manter a motivação.

Mas nem tudo foi tranquilo, principalmente pra quem migra de sistemas mais tradicionais. Os problemas com compartilhamento de tela em aplicativos de videoconferência foram um dos primeiros obstáculos pra mim. A configuração de múltiplos monitores também teve suas peculiaridades: precisei pesquisar e ajustar na mão pra acertar a configuração do meu segundo monitor, e isso quebrou o fluxo de trabalho algumas vezes. O Wi-Fi não se conectava automaticamente e, às vezes, o tema configurado não aparecia, só surgindo depois do comando `hyprctl reload`. Esses problemas foram resolvidos depois que instalei a versão 2.0 com a ISO oficial.

A curva de aprendizado do uso intensivo do teclado e da lógica do gerenciador de janelas em mosaico pode intimidar no começo. E, pra quem precisa de dual boot, a instalação via ISO, que impõe a criptografia de disco, pode ser um obstáculo. A compatibilidade com alguns aplicativos e uma base comunitária ainda menor que outras distros levantam dúvidas sobre suporte a longo prazo, embora a estabilidade de um sistema relativamente novo tenha me impressionado.

No fim, o Omarchy é uma boa opção pra quem valoriza produtividade e estética, mas exige adaptação e paciência pra superar as peculiaridades do Linux moderno. Você pode instalá-lo numa VM só pra testar e, se gostar, migrar pro seu setup principal, assim como eu fiz.

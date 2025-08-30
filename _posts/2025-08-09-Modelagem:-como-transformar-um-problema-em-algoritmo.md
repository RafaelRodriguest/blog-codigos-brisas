---
layout: post
title: 'Antes de escrever código: como transformar um problema em um algoritmo'
author: cotes
date: 2025-08-09 14:00:00 -300
categories: [Programação, Fundamentos]
tags: [algoritmos, lógica, abstração, modelagem]
---

Quando a gente fala de desenvolvimento de software, é comum imaginar a tela preta do terminal, linhas de código coloridas e aquele "rodar sem erros" que dá um certo alívio. Mas, na prática, o primeiro passo não é abrir o editor de código. Antes disso, existe um momento essencial — e que costuma diferenciar bons sistemas de soluções improvisadas: entender o problema e transformá-lo em um algoritmo bem definido.

Algoritmos e lógica de programação são a espinha dorsal de qualquer software. Eles definem a estrutura e o fluxo do sistema sem depender de uma linguagem específica. Nessa fase, descrevemos o comportamento completo do que será construído — entradas, processamento, saídas, condições e até fluxos alternativos — usando representações como pseudocódigo, fluxogramas ou diagramas de estado.

Essa etapa é "linguagem-agnóstica": o que você cria aqui pode ser convertido quase linha a linha para C, Java, Ruby ou qualquer outra. Mais importante que escolher a linguagem certa, é criar uma solução clara e funcional. A linguagem é só a ferramenta; cada uma tem pontos fortes e fracos, seja pelo paradigma que adota, seja pelo desempenho ao compilar ou interpretar.

E tem um conceito que merece destaque (e um post só pra ele): **abstração**. É ela que permite enxergar o sistema de forma ampla, criar uma base sólida e, só depois, traduzir isso para código.

## 1. Entendendo o problema de verdade

Todo software nasce de um problema — mas "ter uma ideia" não é o suficiente. O objetivo precisa estar tão claro que seja impossível confundir o que o sistema vai fazer.

Essa primeira etapa é quase um trabalho de detetive: coletar dados, entender como tudo funciona e mapear restrições. Aqui entram:

- **Entradas**: o que o sistema vai receber.
- **Saídas**: o que ele vai entregar.
- **Regras de negócio**: como o sistema deve se comportar.
- **Exceções**: casos extremos e situações fora do padrão.

Essa investigação não depende só do que você já sabe. Muitas vezes, vai ser preciso conversar com usuários, buscar referências, ler documentação ou até revisitar conceitos que você já conhece. É isso que chamamos de **modelagem do problema**.

## 2. Planejando a solução (sem escrever código ainda)

Com o problema bem modelado, é hora de pensar na solução. E, aqui, o foco é criar uma sequência lógica de passos que leve da situação atual até o resultado esperado.

Não é só uma lista solta de ações: cada passo deve depender do anterior e preparar o próximo. É esse encadeamento que transforma ideias soltas em algo que um computador realmente consegue executar.

## 3. A especificação do algoritmo

O resultado de todo esse trabalho é a **especificação do algoritmo** — um documento que descreve, com clareza, como o problema será resolvido.

Esse documento pode ser superformal, se você estiver numa equipe grande, ou um rascunho rápido, se estiver trabalhando sozinho.A especificações de software é uma parte crucial na engenharia do software, pois nela são definidas todas as necessidades e restrições que irão atender o projeto e merece uma atenção especial em outro momento, mas por enquanto entenda que é importante é que ele sirva de guia para que a implementação seja direta. A partir dele, traduzir para qualquer linguagem de programação se torna muito mais simples.

---

**No próximo post**, vamos colocar essa teoria em prática escrevendo o algoritmo de um problema clássico e fascinante da programação: a **Torre de Hanói**. Um ótimo exemplo para mostrar como modelar, planejar e especificar uma solução antes mesmo de tocar no código.

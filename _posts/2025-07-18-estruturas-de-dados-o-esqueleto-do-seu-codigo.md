---
layout: post
title: 'O Esqueleto do código: Estruturas de dados'
author: cotes
date: 2025-07-18 09:15:00 -300
categories: [Programação, Fundamentos]
tags: [estruturas de dados, algoritmos, eficiência]
---


Se algoritmos são o músculo do código, estruturas de dados são o esqueleto. E você não vai longe sem uma espinha dorsal bem estruturada.

A maioria dos programadores aprende a sintaxe de uma linguagem, usa arrays pra tudo, e acha que isso é suficiente. Spoiler: não é.

Escolher a estrutura de dados errada é como usar uma chave de fenda pra martelar um prego. Tecnicamente funciona, mas é lento, ineficiente e você vai se machucar no processo.

Estruturas de dados são formas organizadas de guardar e acessar informações. Simples assim. Mas essa simplicidade esconde um poder enorme na hora que seu sistema precisa escalar.

Arrays são a estrutura mais básica. Uma sequência de elementos na memória. Você acessa qualquer posição direto. O décimo elemento ou o milésimo, tanto faz. Mesmo tempo.

Mas arrays têm um problema: são rígidos. Inserir um elemento no meio significa empurrar tudo pra frente. Remover significa puxar tudo pra trás. Em arrays grandes, isso é lento demais.

Listas ligadas resolvem esse problema de um jeito elegante. Cada elemento aponta pro próximo. Inserir ou remover é só ajustar os ponteiros. Rápido.

O trade-off é que você perde o acesso direto. Pra chegar no milésimo elemento, precisa percorrer os 999 anteriores. Não existe almoço grátis.

Você escolhe arrays quando precisa acessar elementos por índice. Escolhe listas ligadas quando precisa inserir e remover bastante. É isso.

Pilhas e filas são estruturas que impõem ordem. Uma pilha é tipo aquela pilha de pratos na cozinha. Você sempre pega o de cima. Último a entrar, primeiro a sair.

Filas são como fila de banco mesmo. Primeiro a entrar, primeiro a sair. Nada de furar fila aqui.

Parece básico demais, mas não é. Pilhas são usadas em chamadas de função, no ctrl+z do seu editor, na navegação do navegador. Filas aparecem em impressoras, sistemas de mensagens, processamento de tarefas.

Você implementa pilhas e filas com arrays ou listas ligadas. A interface é que muda.

Árvores são onde as coisas ficam interessantes. Uma estrutura hierárquica. Um nó raiz no topo, filhos abaixo, e assim por diante.

A árvore binária é a mais comum. Cada nó tem no máximo dois filhos: esquerda e direita. E aqui vem a parte legal: se você organiza os valores de forma que o filho esquerdo é sempre menor e o direito sempre maior, buscar fica absurdamente rápido.

Em vez de percorrer todos os elementos, você corta o espaço pela metade a cada passo. Mil elementos? Umas 10 comparações. Um milhão? Umas 20.

É o que torna sistemas grandes viáveis.

Árvores aparecem em tudo. Sistemas de arquivos são árvores. O DOM do navegador é uma árvore. Bancos de dados usam árvores pra indexar dados. Compiladores constroem árvores sintáticas.

Grafos são árvores que se libertaram. Qualquer nó pode se conectar a qualquer outro. Sem hierarquia. Pura liberdade.

Grafos modelam redes. Redes sociais, mapas, internet, circuitos. Qualquer coisa onde existem entidades e conexões entre elas é um grafo.

Você representa grafos com listas de conexões ou matrizes. A escolha depende se tem muita ou pouca conexão entre os nós.

Tabelas hash são provavelmente a estrutura mais útil que existe. Você pega uma chave, joga numa função matemática, e obtém um índice. Guardar e buscar acontece quase instantaneamente.

É por isso que objetos em JavaScript, dicionários em Python, e hashmaps em Java são tão rápidos. Por baixo dos panos, são tabelas hash.

O problema são as colisões. Às vezes duas chaves diferentes geram o mesmo índice. Você resolve com uma lista em cada posição ou procurando a próxima posição livre. Existem formas melhores e piores de lidar com isso, mas todas funcionam.

Heaps são árvores especiais onde o pai é sempre maior (ou menor) que os filhos. Isso garante que o maior (ou menor) elemento está sempre no topo. Perfeito pra fila de prioridade.

Algoritmos de roteamento, escalonadores de sistema operacional, aquele algoritmo do Dijkstra que você viu na faculdade. Todos usam heaps.

Tries são árvores pra texto. Cada nó representa uma letra. Você percorre letra por letra. Pra saber se "casa" existe no dicionário, vai em c, depois a, depois s, depois a.

Autocomplete do seu celular usa trie. Corretor ortográfico usa trie. Sistema de roteamento de URLs usa trie.

O importante é saber qual estrutura resolve seu problema.

Busca rápida pede tabela hash ou árvore binária. Manter ordem funciona bem com árvores ou listas ordenadas. Processamento por prioridade usa heap. Modelar conexões é trabalho pra grafo.

Cada estrutura tem um caso de uso. Cada uma tem seus trade-offs. Velocidade de acesso vs. velocidade de inserção. Uso de memória vs. performance. Simplicidade vs. eficiência.

Programadores ruins usam arrays pra tudo e ficam sem entender por que o código é lento. Programadores bons conhecem as estruturas e sabem quando usar cada uma.

Não existe estrutura perfeita. Existe a estrutura certa pro problema certo.

E isso você só aprende conhecendo as opções. Não precisa implementar tudo do zero toda vez. Mas precisa entender como funcionam, onde travam, onde brilham.

Porque quando seu sistema crescer, quando os dados passarem de milhares pra milhões, quando os usuários reclamarem de lentidão, você vai precisar saber exatamente onde está o gargalo.

E vai precisar de mais do que arrays.

Nos próximos posts vou mostrar implementações práticas. Como usar essas coisas na vida real, não só na teoria da faculdade. Porque teoria sem prática não resolve problema nenhum.

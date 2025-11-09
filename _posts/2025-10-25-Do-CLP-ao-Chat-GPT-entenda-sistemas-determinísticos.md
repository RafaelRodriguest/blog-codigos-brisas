---
layout: post
title: "Do CLP ao Chat GPT: Entenda sistemas determinísticos"
author: cotes
date: 2025-10-25 18:00:00 -0300
categories: [Sistemas, Teorias, Engenharia, Fundamentos]
tags: [Modelos, CLP, Sistemas,Inteligência artificial, Sistemas embarcados]
---

Tem conceito que todo programador deveria entender. Não pra ficar discutindo qual linguagem é melhor ou qual arquitetura tá na moda. Mas pra fazer projeto sério. A natureza do tempo na computação. Como isso impacta o software que você escreve. Temos o determinismo. A ideia de que você pode conhecer e garantir o pior caso e a estocasticidade. A realidade de que a maioria dos sistemas lida com probabilidades, não com certezas. Isso é engenharia pura. E como você lida com isso define a robustez do que você constrói.
Um sistema determinístico é aquele onde, dadas as mesmas entradas e o mesmo estado inicial, você sempre obtém a mesma saída no mesmo tempo. Não provavelmente. Não na maioria das vezes. Sempre. Isso se opõe aos sistemas estocásticos, onde o comportamento incorpora aleatoriedade. Matematicamente, é uma função pura estendida ao domínio temporal. Tanto a saída quanto o tempo são invariantes.

 
  ![FUNCTION_DETERMINISM](assets/img/function_determinism.png)
 

  Pra garantir determinismo, você precisa de três coisas. Primeiro: o tempo de execução de qualquer operação deve ser totalmente previsível. Você precisa do pior cenário absoluto. Segundo: o sistema não pode depender de elementos imprevisíveis. Sem alocação dinâmica. Sem I/O assíncrono descontrolado. Terceiro: tarefas críticas precisam terminar dentro dos deadlines. Sem falta. Essas três garantias juntas permitem que você prove matematicamente o comportamento do sistema.

Quando falamos de sistemas determinísticos, esqueça velocidade. O que importa é previsibilidade. Um sistema determinístico é aquele onde você pode afirmar com certeza: esta operação vai terminar em, no máximo, X unidades de tempo. Ponto. Não é geralmente termina rápido. É o pior caso possível é conhecido e controlado. Tempo real não significa rápido. Significa previsível.

Pense num airbag automotivo. O cálculo de acionamento deve completar em aproximadamente 10 milissegundos após detectar a colisão. Num sistema ABS, o controle opera em ciclos de 100Hz. Atrasar significa perder controle da roda. Não existe média. Não existe "99% das vezes". É garantia absoluta. Essas aplicações exigem que você conheça o comportamento no pior cenário possível.

Agora observe um sistema web típico. Ele é estocástico por natureza. O tempo de resposta é imprevisível. Você não garante tempo máximo absoluto. Apenas observa a média e percentis. O perigo está em confundir essa observação estatística com garantia absoluta. São duas abordagens fundamentalmente diferentes de lidar com tempo.
O Controlador Lógico Programável é exemplo clássico de sistema determinístico. Ele executa sempre o mesmo ciclo de operações, no mesmo tempo, na mesma sequência. Independente das condições externas. Leitura das entradas, execução da lógica, atualização das saídas. Cada fase ocorre em tempos previsíveis. O tempo total do ciclo permanece constante, geralmente entre dez e cem milissegundos. Se esse tempo for ultrapassado, o CLP entra em modo de falha segura.                                         

  ![PLC_SCAN](/assets/img/plc_scan.webp)


O determinismo é essencial porque o CLP interage diretamente com o mundo físico. Um pequeno atraso pode causar falhas mecânicas, perdas de produção ou riscos de segurança. Pra alcançar esse determinismo, o hardware e firmware são propositalmente simplificados. Uma única tarefa de forma linear. Sem multitarefa. Sem sistema operacional de propósito geral. O processador é dedicado exclusivamente à execução da lógica de controle.

Computadores convencionais não são determinísticos. O tempo de execução do mesmo código varia conforme a carga de trabalho, gerenciamento de processos, caches, interrupções. Essa variação é aceitável em sistemas de uso geral, mas incompatível com controle de processos físicos. O CLP não busca desempenho máximo ou flexibilidade. Busca previsibilidade absoluta.
Agora pegue um sistema embarcado. Sistema de freio ABS. Navegação na aviação. Marca-passo. Múltiplas tarefas concorrem pela CPU. Aqui, preempção é crucial. Interromper uma tarefa de baixa prioridade pra dar lugar a uma de alta prioridade. Isso acontece com latências previsíveis na casa dos microssegundos. A arquitetura desses sistemas é projetada pra garantir que a tarefa mais importante sempre execute quando precisa.

![Preemption](assets/img/preemption.jpeg)

No sistema web, preempção significa algo completamente diferente. Seu trabalho pode ser interrompido a qualquer momento, por razões que você não entende. Seu código roda numa JVM, dentro de um container, numa VM, num data center compartilhado. O Garbage Collector decide quando parar o mundo por centenas de milissegundos. O Kubernetes pode mover seu pod quando quiser. O scheduler do Linux está otimizando pra throughput, não pro seu deadline.

E então chegamos à IA. Aqui a confusão atinge outro nível. Você já perguntou ao ChatGPT a mesma coisa duas vezes? Já reparou que a resposta nunca é exatamente igual? Que às vezes ele responde em 2 segundos, outras em 15? Não é bug. É exatamente como foi projetado. ChatGPT, Claude, Gemini. Todos os LLMs modernos são modelos probabilísticos. 

![LLM_WORK](assets/img/LLM_WORK.png)

Eles não calculam respostas. Eles amostram de distribuições de probabilidade. Cada palavra que você recebe é resultado de um sorteio ponderado entre milhares de possibilidades. As pessoas não entendem isso. Elas veem o ChatGPT respondendo rápido na maioria das vezes e assumem que é confiável. Assumem que podem integrá-lo em sistemas críticos. Assumem que se funciona no teste, funcionará em produção da mesma forma.

LLMs são ferramentas incríveis pro que foram projetados: gerar texto plausível, resumir informações, auxiliar em tarefas criativas. Mas foram construídos sobre uma fundação de probabilidade, não de certeza. Você não pode garantir que a mesma entrada sempre produzirá a mesma saída. Você não pode certificar o comportamento de um sistema que fundamentalmente opera através de probabilidades. Isso não é uma limitação técnica temporária. É a natureza fundamental dessas tecnologias.
E não são só os LLMs. Redes neurais pra visão computacional têm o mesmo problema. Mesma imagem, hardware diferente, resultados ligeiramente diferentes. Sistemas de reconhecimento de voz são completamente não determinísticos. Dependem do ruído ambiente, da velocidade da fala, do sotaque. A indústria está tentando usar essas tecnologias em contextos onde não-determinismo é inaceitável.

Você não coloca LLM no caminho crítico. Você o usa pra sugerir, nunca pra comandar. Um sistema de automação industrial pode usar IA pra detectar anomalias nos dados históricos e alertar humanos. Mas jamais pra tomar decisões de controle em tempo real. Um sistema médico pode usar IA pra auxiliar diagnóstico, mas a decisão final passa por algoritmos determinísticos e humanos. A ferramenta certa pro contexto certo.

No final, a arquitetura do seu sistema depende de uma pergunta simples: qual o custo de uma única operação falhar no pior momento possível? Se a resposta incluir morte, lesão, perda financeira catastrófica ou dano ambiental irreversível, você precisa de determinismo. Esqueça o garbage collector. Prepare-se pra garantir cada microssegundo. Deixe a IA como ferramenta de análise offline, como auxiliar de decisão humana. Nunca como controlador direto.

Se a resposta for um usuário irritado ou atraso sem importância, então o mundo estocástico funciona. Use as ferramentas modernas, incluindo LLMs e redes neurais. Você não precisa evitar IA. Você precisa entender sua natureza e projetar sistemas que a usem apropriadamente. Reconhecer que um LLM é ferramenta probabilística incrível pra certos problemas, e completamente inadequada pra outros.
Velocidade na maioria dos casos não substitui garantias no pior caso. A diferença entre essas escolhas, em alguns sistemas, define se alguém vive ou morre. Saber qual é qual define que tipo de engenheiro você é.

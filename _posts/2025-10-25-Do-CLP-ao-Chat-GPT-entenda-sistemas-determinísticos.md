---
layout: post
title: "Do CLP ao Chat GPT: Entenda sistemas determinísticos"
author: cotes
date: 2025-10-25 18:00:00 -0300
categories: [Sistemas, Teorias, Engenharia, Fundamentos]
tags: [Modelos, CLP, Sistemas,Inteligência artificial, Sistemas embarcados]
---

Existem conceitos que todo programador deveria entender para ser um desenvolvedor melhor e também para ele fazer projetos melhores e sérios de software. Ao invés de estar em discussões inúteis sobre é sobre qual linguagem é melhor, ou qual arquitetura está na moda, poderia estar entendendo sobre algo mais fundamental: a natureza do tempo na computação e seus impactos no contexto do seu projeto de software. 

De um lado, o determinismo: a ideia de que você pode conhecer e garantir o pior caso. Do outro, a estocasticidade: a realidade de que a maioria dos sistemas lida com probabilidades, não com certezas. 

Isso é engenharia pura. E a forma como programadores lidam com isso ou deixam de lidar define a robustez dos sistemas que construímos. 

# A Essência do Determinismo Computacional 

Um sistema determinístico é aquele onde, dadas as mesmas entradas e o mesmo estado inicial, você sempre obtém a mesma saída no mesmo tempo. Não "provavelmente". Não "na maioria das vezes". Sempre. 

Matematicamente, é uma função pura estendida ao domínio temporal. Tanto a saída quanto o tempo são invariantes para as mesmas condições iniciais. Isso se opõe radicalmente aos sistemas estocásticos, onde o comportamento incorpora aleatoriedade intrínseca—seja por design, seja por limitações arquiteturais. 

 
  ![FUNCTION_DETERMINISM](assets/img/function_determinism.png)
 

Para garantir a previsibilidade total de um sistema (o determinismo), precisamos de três garantias. A primeira: o tempo de execução de qualquer operação deve ser totalmente previsível e nunca exceder um limite máximo conhecido. Não basta saber o tempo médio ou o mais comum; precisamos do pior cenário absoluto (o "teto"). Isso inclui contabilizar tudo (do maior número de passos no código a problemas de memória). Usamos técnicas de análise para provar matematicamente que esse tempo máximo é real e nunca será ultrapassado. 

Segundo o sistema não pode depender de elementos intrinsecamente imprevisíveis. Sem alocação dinâmica, porque malloc() pode demorar tempos variáveis dependendo da fragmentação do heap. Sem I/O não bloqueante assíncrono, porque operações devem ser síncronas ou com timeouts rígidos. Sem dependência de recursos compartilhados não controlados como mutexes sem prioridade, filas sem limites ou pools sem reservas. 

Terceiro, tarefas críticas precisam ser finalizadas dentro de seus deadlines sem falta.Para viabilizar essa garantia, o sistema requer um scheduler que funcione de forma previsível, utilizando métodos como Rate-Monotonic. Essa organização deve ser validada por uma análise de escalonabilidade que nos dá a prova matemática de que todos os prazos são alcançáveis. Além disso, para evitar que tarefas menos importantes atrapalhem as cruciais, é crucial o uso de protocolos (Priority Ceiling, por exemplo) que controlam e impedem a inversão de prioridade. 

# A Ilusão da Velocidade vs. a Certeza do Pior Caso 



Quando falamos de sistemas determinísticos, esqueça velocidade. O que importa é previsibilidade. Um sistema determinístico é aquele onde você pode afirmar com certeza: "esta operação vai terminar em, no máximo, X unidades de tempo". Ponto. Não é "geralmente termina rápido", mas "o pior caso possível é conhecido e controlado". 

É por isso que "tempo real" é tão mal intendido. Na indústria, tempo real não significa rápido—significa previsível. E isso se traduz em deadlines com consequências radicalmente diferentes. Em sistemas hard real-time, falhar um deadline não é apenas inconveniente—é uma falha total do sistema. O valor da computação cai para zero após o deadline. Pense num airbag automotivo onde o cálculo de acionamento deve completar em aproximadamente 10 milissegundos após a colisão ser detectada, ou num sistema ABS onde o ciclo de controle opera em 100Hz. Atrasar significa perder controle da roda. Não existe média. Não existe "99% das vezes". É uma garantia determinística absoluta. 

Em sistemas soft real-time, falhar deadlines degrada a qualidade do serviço, mas não causa falha catastrófica. Pense em streaming de vídeo (onde frames atrasados causam pequenas travadas) ou jogos (frame drops). O sistema consegue tolerar violações ocasionais de prazo, mas ainda assim se beneficia muito de ter um comportamento previsível (determinístico) na maior parte do tempo. 

Em contraste, observe um sistema web típico. Ele é aleatório (estocástico) por natureza. O tempo de resposta é uma variável imprevisível. Você não garante um tempo máximo absoluto; apenas observa a média e o tempo que a maioria das requisições leva para terminar (os percentis). O perigo está exatamente em confundir essa observação estatística com a garantia absoluta exigida pelos sistemas críticos. 

 

# Como modelos determinísticos funcionam em cada contexto? 

 

O Controlador Lógico Programável (CLP) é um exemplo clássico de sistema determinístico. Ele foi projetado para executar sempre o mesmo ciclo de operações, no mesmo tempo e na mesma sequência, independentemente das condições externas. 

  

Seu funcionamento é dividido em etapas fixas: leitura das entradas, execução da lógica de controle, atualização das saídas e tarefas auxiliares de comunicação e diagnóstico. Cada uma dessas fases ocorre em tempos previsíveis e controlados. O tempo total do ciclo é a soma dessas etapas e permanece constante dentro de limites definidos, geralmente entre dez e cem milissegundos, conforme a aplicação. Se esse tempo for ultrapassado, o CLP entra em modo de falha segura para garantir a integridade do processo. 

O determinismo é essencial porque o CLP interage diretamente com o mundo físico. Cada decisão de controle depende de leituras precisas e respostas dentro de janelas de tempo exatas. Em processos industriais, um pequeno atraso pode causar falhas mecânicas, perdas de produção ou riscos de segurança. Por isso, o comportamento do CLP deve ser previsível e repetitivo, sem variação temporal. Esta exigência é crítica em aplicações de motion control, como o sincronismo de eixos em máquinas e robótica, onde tempos de ciclo curtos e atualização precisa de saídas são fundamentais. 

Para alcançar esse nível de determinismo, o hardware e o firmware do CLP são propositalmente simplificados. Ele executa uma única tarefa de forma linear, sem multitarefa, sem escalonamento de threads e sem sistema operacional de propósito geral. O firmware é o próprio sistema operacional, e o processador é dedicado exclusivamente à execução da lógica de controle. Além disso, suas entradas e saídas são soladas e filtradas, reduzindo interferências elétricas que poderiam comprometer a consistência temporal. A comunicação com dispositivos de campo também segue esse princípio, sendo frequentemente realizada por meio de protocolos industriais deterministicos, como EtherCAT e Profinet, que garantem a transmissão e recepção de dados dentro de janelas de tempo estritamente controladas. 

Em contraste, os computadores convencionais não são determinísticos. O tempo de execução de um mesmo código pode variar conforme a carga de trabalho, o gerenciamento de processos, caches, interrupções e tarefas em segundo plano. Essa variação é aceitável em sistemas de uso geral, mas incompatível com o controle de processos físicos, onde o tempo de resposta precisa ser garantido. 

O determinismo do CLP é o que o diferencia da computação convencional. Ele não busca desempenho máximo ou flexibilidade, mas previsibilidade absoluta. Essa característica garante que cada ciclo de controle ocorra no tempo exato esperado, tornando o sistema confiável e seguro.                                            

  ![PLC_SCAN](/assets/img/plc_scan.webp)


Agora, pegue um sistema embarcado como um sistema de freio ABS ou sistema de navegação na aviação, ou um marca passo. Múltiplas tarefas concorrem pela CPU. Aqui, preempção é crucial. Preempção é a capacidade de interromper uma tarefa de baixa prioridade para dar lugar a uma de alta prioridade. Em um RTOS como VxWorks ou FreeRTOS, isso acontece com latências previsíveis na casa dos microssegundos, tipicamente entre 5 e 50 microssegundos. 

A arquitetura desses sistemas é fundamentada em quatro pilares: kernel totalmente preemptível, onde todo o núcleo pode ser interrompido; escalonamento por prioridades estritas, garantindo que a tarefa mais crítica sempre execute; controle de inversão de prioridade através de protocolos como herança de prioridade; e comunicação síncrona previsível entre tarefas. Juntos, esses princípios permitem calcular e garantir o pior tempo de execução de todas as operações, requisito fundamental para certificação em setores de missão crítica. 


![Preemption](assets/img/preemption.jpeg)

 

No sistema web, a "preempção" significa "seu trabalho pode ser interrompido a qualquer momento, por razões que você não entende". Seu código roda em uma JVM, dentro de um container, em uma VM, em um data center compartilhado. O Garbage Collector decide quando parar o mundo por centenas de milissegundos. O Kubernetes pode mover seu pod quando quiser. O scheduler do Linux está otimizando para throughput, não para seu deadline. 

 

# IA e a Grande Ilusão do Determinismo  

E então chegamos à IA. E aqui a confusão atinge seu ápice. Você já perguntou ao ChatGPT a mesma coisa duas vezes? Já reparou que a resposta nunca é exatamente igual? Já notou que às vezes ele responde em 2 segundos, outras vezes em 15? Isso não é bug. É exatamente como foi projetado. O ChatGPT, o Claude, o Gemin e odos os LLMs modernos são modelos probabilísticos. Eles não calculam respostas. Eles amostram de distribuições de probabilidade. Cada token, cada palavra que você recebe é o resultado de um sorteio ponderado entre milhares de possibilidades. Quando você faz uma pergunta, o modelo não está "pensando deterministicamente". Ele está calculando: "dado tudo que vi até agora, qual a probabilidade de cada próxima palavra?". E então ele escolhe. Às vezes de forma gulosa (pegando sempre a mais provável), às vezes de forma estocástica.  Depois quero escrever um texto ou vídeo falando mais sobre esse processo. 

Aí que a parada fica doida, porque as pessoas não entendem isso. Elas veem o ChatGPT respondendo rápido na maioria das vezes e assumem que é confiável. Assumem que podem integrá-lo em sistemas críticos. Assumem que se funciona no teste, funcionará em produção da mesma forma. 

LLMs são ferramentas incríveis para o que foram projetados: gerar texto plausível, resumir informações, auxiliar em tarefas criativas. Mas eles foram construídos sobre uma fundação de probabilidade, não de certeza. De amostragem, não de cálculo. De "bom o suficiente na maioria das vezes", não de "sempre correto". 

Você não pode provar o WCET de uma inferência de LLM. Você não pode garantir que a mesma entrada sempre produzirá a mesma saída. Você não pode certificar o comportamento de um sistema que fundamentalmente opera através de distribuições probabilísticas. 

![LLM_WORK](assets/img/LLM_WORK.png)

E não são só os LLMs. Redes neurais para visão computacional têm o mesmo problema. Mesma imagem, hardware diferente, resultados ligeiramente diferentes. Mesma imagem, momento diferente, tempo de inferência variável. Sistemas de reconhecimento de voz?Completamente não determinísticos e dependem do ruído ambiente, da velocidade da fala, do sotaque, de fatores que você não controla. 

A indústria está empolgada. "IA em tudo!" é o grito de guerra. Mas o que vejo é uma geração de engenheiros que não entende a natureza fundamental dessas tecnologias tentando enfiá-las em contextos onde a não-determinismo é inaceitável. 

Você não coloca o LLM no caminho crítico. Você o usa para sugerir, nunca para comandar. Um sistema de automação industrial pode usar IA para detectar anomalias nos dados históricos e alertar humanos. Mas jamais para tomar decisões de controle em tempo real. Um sistema médico pode usar IA para auxiliar diagnóstico, mas a decisão final e a verificação passam por algoritmos determinísticos e, claro, por humanos. 

# O desenvolvedor que decide

No final, a arquitetura do seu sistema depende de uma pergunta simples: qual o custo de uma única operação falhar no pior momento possível? 

Se a resposta incluir morte, lesão, perda financeira catastrófica ou dano ambiental irreversível, bem-vindo ao mundo do determinismo. Abrace o RTOS, esqueça o garbage collector, e prepare-se para a batalha por cada microssegundo previsível. E deixe a IA onde ela pertence que é como ferramenta de análise offline, como auxiliar de decisão humana, como sistema de suporte mas nunca como controlador direto. Mas se a resposta for "um usuário irritado" ou "experiência degradada", então o mundo estocástico é seu parque de diversões. Use as ferramentas modernas, incluindo LLMs e redes neurais. 

Você não precisa evitar IA. Você precisa entender sua natureza e projetar sistemas que a usem apropriadamente. Você precisa reconhecer que um LLM é uma ferramenta probabilística incrível para certos problemas, e completamente inadequada para outros. Você precisa aceitar que velocidade na maioria dos casos não substitui garantias no pior caso. A diferença entre essas escolhas, em alguns sistemas, define se alguém vive ou morre. Em outros, restrições de tempo não tem tanta relevância assim. 

Saber qual é qual ,isso define que tipo de engenheiro você é.


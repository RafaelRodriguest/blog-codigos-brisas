---
layout: post
title: 'Aleatoriedade não é um detalhe: o caso Coinkite'
author: cotes
date: 2026-08-09 00:34:00 -0300
categories: [Programação, Fundamentos]
tags: [criptografia, bitcoin, aleatoriedade, entropia, segurança]
---

Em agosto a Coinkite, fabricante da hardware wallet Coldcard, soltou um comunicado que fez muita gente do mundo Bitcoin ficar preocupado. Algumas versões do firmware da Coldcard geraram *seeds* com entropia reduzida, ou seja, aquelas chaves privadas que deveriam ser praticamente impossíveis de adivinhar vieram bem mais fracas do que o prometido, e o resultado foi diversas carteiras sendo esvaziadas por conta disso.

O que mais me chama atenção nessa história não é o prejuízo em si, mas a natureza do erro. Não foi senha vazada e nem phishing. Foi o próprio dispositivo, aquele que você compra justamente pra proteger seu segredo, gerando um segredo ruim de fábrica.

> ![Comunicado oficial da Coinkite sobre a falha de entropia](/assets/img/coinkite/comunicado-coinkite.webp)

Pra entender como uma coisa dessas acontece, e por que ela é bem mais comum do que parece, a gente precisa voltar num assunto que achamos que entendemos, mas talvez não entendemos tão bem assim: aleatoriedade. Vou construir esse raciocínio do zero, e quando ele estiver bem montado, a gente volta pro caso da Coinkite e tudo vai fazer sentido.

## **O computador não sabe sortear**

Por design, um computador é um circuito lógico determinístico, isso significa que você dá a mesma entrada, ele roda as mesmas instruções e devolve a mesma saída, sempre, sem exceção. Ele não tem livre-arbítrio nem imaginação pra inventar um número do nada, ele só executa o que foi mandado.

O detalhe é que quase toda linguagem de programação te entrega uma função de "sorteio", o famoso `rand()`, o `Math.random()` e seus parentes, e o nome dessas funções engana um pouco. Elas não são aleatórias de verdade, são equações matemáticas que pegam um valor inicial, chamado de semente, e a partir dele geram uma sequência comprida o suficiente pra parecer embaralhada aos olhos de um ser humano.

O nome técnico é bem mais honesto que o coloquial: gerador *pseudoaleatório*. Entenda esse "pseudo", ele está ali de propósito, porque aquilo é apenas uma aleatoriedade fake, não é real.

Com isso, podemos entender que se você inicializar o mesmo gerador duas vezes com a mesma semente, ele vai cuspir exatamente a mesma sequência de números "sorteados" nas duas vezes. Aquela bagunça toda é só aparência, porque por baixo dela é tudo previsível, do primeiro ao último dígito.

<div style="border:1px solid #00cc00; border-radius:6px; padding:1rem 1.25rem; margin:1.5rem 0; font-family:'Space Grotesk',sans-serif;">
  <div style="display:flex; align-items:center; gap:.75rem; flex-wrap:wrap; margin-bottom:.6rem;">
    <span style="border:1px solid #00cc00; border-radius:4px; padding:.15rem .5rem; color:#00ff00;">semente = 42</span>
    <span style="color:#00cc00;">→</span>
    <span style="border:1px solid #00cc00; border-radius:4px; padding:.15rem .5rem; color:#00ff00;">rand()</span>
    <span style="color:#00cc00;">→</span>
    <span style="color:#c8c8d2; font-family:monospace;">7, 3, 9, 1, 4, 2 …</span>
  </div>
  <div style="display:flex; align-items:center; gap:.75rem; flex-wrap:wrap;">
    <span style="border:1px solid #00cc00; border-radius:4px; padding:.15rem .5rem; color:#00ff00;">semente = 42</span>
    <span style="color:#00cc00;">→</span>
    <span style="border:1px solid #00cc00; border-radius:4px; padding:.15rem .5rem; color:#00ff00;">rand()</span>
    <span style="color:#00cc00;">→</span>
    <span style="color:#c8c8d2; font-family:monospace;">7, 3, 9, 1, 4, 2 …</span>
  </div>
  <p style="color:#c8c8d2; margin:.75rem 0 0; font-size:.9rem;">Mesma semente, mesma saída. O "acaso" é reprodutível — e o que é reprodutível é adivinhável.</p>
</div>

## **Onde a imitação basta e onde ela custa caro**

Pra um jogo, uma animação ou uma simulação estatística qualquer, essa aleatoriedade fajuta resolve muito bem, e está tudo certo. Ninguém vai perder tempo reconstruindo a semente do seu Tetris pra prever a próxima peça, e mesmo que reconstruísse, não faria diferença nenhuma na vida de ninguém.

Criptografia joga em outro nível. Se o atacante descobre a fórmula por trás da sequência, ou consegue deduzir de onde saiu a semente, ele passa a prever com precisão quais serão as próximas chaves geradas, quebrando a segurança desse sistema.

No Bitcoin isso é importante por um motivo bem específico: quem tem a chave privada é dono dos fundos, ponto. Não existe cadastro ou e-mail de recuperação que traga seu bitcoin de volta depois que ele for roubado, a segurança do seu dinheiro se apoia num fator único, que é a sua chave privada precisar ser um segredo tão bem guardado que ninguém no universo consiga adivinhar.

Junte as duas pontas e o problema aparece sozinho, um segredo que precisa ser impossível de adivinhar sendo produzido por uma função que, por natureza, é previsível.

## **Ninguém quebra a matemática, quebram a origem**

Hacker sério não fica tentando quebrar a matemática do Bitcoin na força bruta pura, porque o espaço de chaves é grande demais e isso não fecha em tempo humano, então o ataque não é contra o cofre, é contra a fábrica do cofre.

Imagine que o software usou a hora do sistema em milissegundos como semente pra gerar a carteira. O atacante não precisa testar infinitas combinações, ele só precisa rodar um script varrendo os milissegundos daquele dia específico, e pronto, aquele "impossível de adivinhar" encolheu pra algumas horas de processamento numa máquina qualquer.

É essa a ideia central que eu quero que fique: aleatoriedade falsa diminui o tamanho do cofre. Você acredita ter uma fechadura de milhões de combinações e, na prática, tem umas poucas centenas de milhares.

Foi exatamente pra resolver isso que as hardware wallets sérias, como Ledger, Trezor e a própria Coldcard, pararam de confiar nas funções de software. Elas carregam um chip dedicado, o TRNG (*True Random Number Generator*), que em vez de resolver uma equação, mede o ruído elétrico microscópico e caótico dos próprios componentes físicos, e é isso que gera entropia de verdade, imprevisível. São componentes físicos entrando pra cobrir o limite da matemática.

<div style="border:1px solid #00cc00; border-radius:6px; padding:1rem; margin:1.5rem 0; font-family:'Space Grotesk',sans-serif;">
  <div style="display:flex; gap:1rem; flex-wrap:wrap;">
    <div style="flex:1; min-width:220px;">
      <p style="color:#00ff00; font-weight:700; margin:0 0 .5rem;">PSEUDOALEATÓRIO (software)</p>
      <p style="color:#c8c8d2; margin:0;">semente → equação → sequência previsível. Mesma semente, mesma saída. Sempre.</p>
    </div>
    <div style="flex:1; min-width:220px;">
      <p style="color:#00ff00; font-weight:700; margin:0 0 .5rem;">TRNG (chip físico)</p>
      <p style="color:#c8c8d2; margin:0;">ruído elétrico → entropia real → imprevisível. O caos da física, não da matemática.</p>
    </div>
  </div>
</div>

## **A ponte que quebrou na Coldcard**

> ![Hardware wallet Coldcard e seu chip gerador de entropia](/assets/img/coinkite/coldcard.webp)

Com o conceito montado, o caso Coinkite se resume nisso: um erro no firmware fez o dispositivo ignorar o TRNG e cair de volta num gerador por software, ou seja, o caos da física que inseria uma boa entropia foi trocado pela previsibilidade da matemática, sem ninguém perceber.

Os números do comunicado oficial mostram o tamanho do buraco. As *seeds* geradas nas Mk4, Mk5 e Q afetadas podiam ter cerca de 72 bits de entropia, no lugar dos 128 bits esperados, e isso parece pouca coisa até você lembrar que a escala é exponencial, onde cada bit a menos corta o espaço de busca pela metade, então cinquenta e seis bits a menos não é um arranhão, é um abismo.

<div style="border:1px solid #00cc00; border-radius:6px; padding:1rem 1.25rem; margin:1.5rem 0; font-family:'Space Grotesk',sans-serif;">
  <div style="margin-bottom:.75rem;">
    <p style="color:#00ff00; margin:0 0 .3rem; font-weight:700;">Esperado — 128 bits</p>
    <div style="background:#00ff00; height:14px; width:100%; border-radius:3px;"></div>
    <p style="color:#c8c8d2; margin:.3rem 0 0; font-size:.85rem; font-family:monospace;">≈ 340.000.000.000.000.000.000.000.000.000.000.000.000 combinações</p>
  </div>
  <div>
    <p style="color:#00ff00; margin:0 0 .3rem; font-weight:700;">Gerado com a falha — 72 bits</p>
    <div style="background:#00cc00; height:14px; width:56.25%; border-radius:3px; opacity:.6;"></div>
    <p style="color:#c8c8d2; margin:.3rem 0 0; font-size:.85rem; font-family:monospace;">≈ 4.700.000.000.000.000.000.000 combinações</p>
  </div>
  <p style="color:#c8c8d2; margin:.75rem 0 0; font-size:.9rem;">A barra parece só um pouco menor. O espaço de busca real ficou cerca de 72 quatrilhões de vezes mais fácil de varrer.</p>
</div>

O problema atingiu versões específicas, e vale registrar quais: Mk2/Mk3 nas versões 4.0.1 a 4.1.9, Mk4/Mk5 antes da 5.6.0 (ou 6.6.0X nas versões *Edge*), e a Coldcard Q antes da 1.5.0Q (ou 6.6.0QX nas *Edge*). No caso das Mk2/Mk3, a *seed* do período era considerada de risco quando o usuário não tinha adicionado entropia própria por fora.

E tem uma consequência dessa falha que precisa ficar bem clara na cabeça de quem usa esse tipo de aparelho. Atualizar o firmware conserta a geração futura de chaves, mas não conserta uma *seed* velha que já foi criada, então a carteira comprometida continua comprometida do mesmo jeito. Não é um bug que some ao reiniciar o aparelho, é um segredo que nasceu fraco e vai carregar essa fraqueza pra sempre.

## **A saída é um cubo de plástico**

> ![50 lançamentos de um dado geram entropia suficiente](/assets/img/coinkite/dado-entropia.webp)

A própria Coinkite aponta que pelo menos 50 lançamentos de um dado justo já forneceriam entropia suficiente pra blindar contra esse problema específico.

Pessoal, vale parar nisso um segundo e sentir a ironia. A correção pra uma falha de software de última geração é um cubo de plástico numerado que a humanidade usa há milênios, e ele funciona porque não roda equação, não tem semente, não guarda estado interno pra um atacante reconstruir depois, ele é caos físico puro e imprevisível, e é justamente por isso que resolve.

<div style="border:1px solid #00cc00; border-radius:6px; padding:1rem 1.25rem; margin:1.5rem 0; font-family:'Space Grotesk',sans-serif; text-align:center;">
  <p style="color:#00ff00; font-weight:700; margin:0 0 .25rem;">50 lançamentos ≈ 129 bits de entropia</p>
  <p style="color:#c8c8d2; margin:0; font-size:.9rem;">Cada lançamento de um dado justo (1 em 6) rende ≈ 2,58 bits. 50 deles superam com folga os 128 bits que a máquina deveria ter gerado sozinha — e nenhum atacante consegue reconstruir a sua mão.</p>
</div>

No fundo é a mesma lição do chip TRNG, só que na palma da mão. Uma coisa importante de dizer é: o problema nunca foi a máquina usar matemática, foi de onde ela tira a semente. A imprevisibilidade de verdade precisa nascer de um evento físico, do ruído, do caos do mundo lá fora, só que basta uma dose pequena disso, porque a partir de uma boa semente a própria máquina consegue esticar esse acaso com segurança, usando um gerador criptográfico, o CSPRNG, que é software mas foi feito pra continuar imprevisível mesmo sob ataque. Os 50 lançamentos do dado são exatamente isso, você entrega a semente física e a matemática forte cuida de todo o resto.

Nesse sentido, aquele `random()` que você chama no automático não é algo totalmente do acaso, é um gerador estatístico simples, o tipo errado pra segurança, feito pra parecer aleatório e não pra resistir a um atacante, e na esmagadora maioria dos casos ele dá conta e ninguém sente falta. Mas no dia em que o número sorteado for a única coisa protegendo algo que realmente importa, é bom você saber exatamente de onde ele veio, porque foi ignorar essa pergunta que custou o dinheiro de gente que confiava no aparelho.

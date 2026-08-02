---
description: Transforma um rascunho com ideias brutas em um post completo do blog Código 404, respeitando a linha editorial, estrutura e voz do autor.
---

# Skill: novo-post

## O que esta skill faz

O usuário cria um arquivo `.md` em `_posts/` (ou `_drafts/`) com ideias, tópicos, frases soltas ou um texto parcial. Esta skill lê esse arquivo, completa o conteúdo e o reescreve no formato final publicável — mantendo a voz do autor e seguindo todas as regras editoriais do blog.

## Como usar

1. Crie um arquivo em `_drafts/` ou `_posts/` com o nome no formato `YYYY-MM-DD-slug-do-post.md`
2. Escreva livremente: ideias, tópicos, frases que quer usar, argumento central, exemplos
3. Chame `/novo-post` ou peça "complete esse post"
4. A skill lê o arquivo, completa e salva o resultado no mesmo arquivo

---

## Fluxo de execução

1. **Localizar o arquivo**: procure o `.md` mais recente em `_drafts/` ou um arquivo indicado pelo usuário
2. **Ler o rascunho**: entenda o argumento central, os tópicos e o tom pretendido
3. **Consultar posts de referência**: leia pelo menos 2 posts de `_posts/` para calibrar voz e estilo
4. **Redigir o post completo**: aplique todas as regras abaixo
5. **Salvar**: sobreescreva o arquivo com o post finalizado
6. **Reportar**: informe o título escolhido, seções criadas e se há algo que o usuário deve revisar

---

## Regras do front matter

Todo post deve começar exatamente assim:

```yaml
---
layout: post
title: 'Título do Post'
author: cotes
date: YYYY-MM-DD HH:MM:SS -0300
categories: [Categoria]
tags: [tag1, tag2, tag3]
---
```

- `title`: direto, provocativo ou afirmativo — nunca genérico ("Como aprender X") nem clickbait vazio
- `categories`: máximo 3, com inicial maiúscula. Use as já existentes no blog: `Programação`, `Carreira`, `Fundamentos`, `Reflexões`, `Aprendizado`, `Tecnologia`
- `tags`: 3 a 5 tags em minúsculas
- `author: cotes` — sempre

---

## Regras de estrutura do post

### Abertura (obrigatória, sem heading)

- Os primeiros 1 a 3 parágrafos NÃO têm heading (`##`)
- Função: criar tensão, apresentar o problema ou fazer uma afirmação forte que prende o leitor
- Tom: direto, sem enrolação, sem "Neste post vamos ver..."
- Deve fazer o leitor querer continuar

**Exemplo de abertura boa:**
> "A maioria das pessoas trata aprender como uma fase. Algo que você faz na escola, na faculdade, talvez num curso profissionalizante. Depois você 'está pronto' e vai trabalhar com o que aprendeu."

**Evite:**
> "Neste artigo, vamos explorar como..." / "Olá, hoje vou falar sobre..."

### Seções

- Títulos de seção: `## **Título em negrito**`
- Subtítulos: `### **Subtítulo em negrito**`
- Sub-subtítulos: `#### **Sub-subtítulo**`
- Mínimo de 3 seções por post, máximo de 6
- Cada seção deve avançar o argumento — não é lista de tópicos, é raciocínio em desenvolvimento

### Parágrafos

- Curtos: 2 a 4 frases por parágrafo
- Um ou dois parágrafos de transição entre seções quando necessário
- Nunca "parede de texto" — se um parágrafo tem mais de 6 linhas, quebre
- Sem marcadores (`-`, `*`) no corpo do texto — o argumento deve fluir em prosa
- Listas são permitidas apenas para enumerações técnicas (ex: estruturas de dados, passos de configuração)

### Encerramento

- O último parágrafo deve ser uma conclusão com posição clara do autor
- Pode ser provocativo, um desafio ao leitor, ou uma síntese da tese central
- NÃO use heading para o encerramento — flui naturalmente do último trecho
- Nunca termine com "Espero que tenha gostado" ou frases de agradecimento

---

## Voz e tom — regras inegociáveis

### O que define a voz do blog

- **Direto e opinionado**: o autor tem posição. Não "existem diferentes opiniões sobre X", mas "X é assim, e quem acha diferente está ignorando Y"
- **Informal mas denso**: linguagem de conversa, mas com substância real — sem superficialidade
- **Sem didatismo condescendente**: não explique o óbvio. O leitor é inteligente
- **Autocrítico e honesto**: o autor fala da própria experiência, admite limitações, não prega do altar
- **Sem motivação vazia**: nada de "acredite em você!", "o sucesso está ao seu alcance!" — o blog é realista

### Construções a evitar

| Evitar | Substituir por |
|---|---|
| "É importante ressaltar que..." | Diga diretamente o que é importante |
| "Como mencionamos anteriormente..." | Não mencione, retome o argumento naturalmente |
| "Neste contexto..." | Corte. Vá direto |
| "De certa forma..." | Ou é de uma forma ou não é — seja específico |
| "Podemos concluir que..." | Conclua sem avisar que vai concluir |
| Adjetivos vagos: "incrível", "revolucionário", "fantástico" | Descreva o que é concreto |

### O que manter da voz do autor

- Expressões coloquiais em português: "pessoal", "entenda esse conceito", "não para por aí"
- Pausas dramáticas com frases curtas: "E dá mesmo. Por um tempo." / "Sempre."
- Referências a experiência pessoal: "em minhas observações", "aprendi em todas as experiências que tive"
- Interpelação direta ao leitor: "se você quer X, então Y"

---

## Regras de ortografia e língua

- Idioma: **português (pt-BR)**
- Termos técnicos em inglês mantidos em itálico: *framework*, *trade-off*, *debug*, *bootcamp*
- Grafias específicas deste blog:
  - `algoritmos` — sem acento (não *algorítmos*)
  - `videoaulas` — uma palavra (não *vídeo-aulas*)
  - `eletricistas` — sem acento (não *elétricistas*)
- Não use `ç` onde não existe na norma culta
- Vírgulas de aposto e enumeração: siga a norma culta, mas o autor usa vírgula antes de "mas", "e" quando há pausa natural — respeite esse estilo

---

## Regras de imagens

- Se o rascunho mencionar uma imagem ou o tema se beneficiar de uma, inclua:
  ```markdown
  > ![descricao](/assets/img/nome-do-arquivo.webp)
  ```
- O caminho **sempre começa com `/assets/img/`** (barra inicial obrigatória)
- Se não há imagem disponível, não inclua placeholder — apenas omita

---

## Extensão ideal

- Posts curtos: 400–600 palavras (reflexões, opiniões diretas)
- Posts médios: 700–1000 palavras (análises, tutoriais conceituais)
- Posts longos: 1000–1500 palavras (histórias completas, temas complexos)
- Nunca force extensão — termine quando o argumento terminar

---

## Checklist antes de salvar

- [ ] Front matter completo e correto
- [ ] Abertura sem heading, com gancho forte
- [ ] Mínimo 3 seções com `## **Título**`
- [ ] Parágrafos curtos, sem parede de texto
- [ ] Voz direta e opinionada — sem genérico, sem motivacional vazio
- [ ] Termos em inglês em itálico
- [ ] Ortografia pt-BR correta (checar as grafias específicas)
- [ ] Encerramento sem heading, com posição clara
- [ ] Nenhuma frase de agradecimento ou "espero que tenha curtido"

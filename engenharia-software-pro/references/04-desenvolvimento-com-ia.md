# Desenvolvimento com IA e Mentalidade de Produto

Síntese de: *Indo Além da Vibe Coding (de programador a desenvolvedor de software na era da
IA)*, *O Engenheiro de Software com Mentalidade de Produto*, *Programação Utilizando IA* e
*IA Generativa para Desenvolvimento de Software*.

## Índice
- Além da vibe coding: de gerar código a fazer engenharia
- Usar IA bem em cada etapa
- Revisar e confiar (com verificação) na saída da IA
- Mentalidade de produto: construir a coisa certa
- O novo perfil do desenvolvedor

---

## Além da vibe coding: de gerar código a fazer engenharia

"Vibe coding" é pedir à IA, colar o que sai e torcer pra funcionar. Funciona para protótipos
e trava em sistemas reais. A tese de *Indo Além da Vibe Coding* é que a IA **eleva** o valor
do que sempre foi engenharia de software de verdade — e desvaloriza o que era só digitar
código.

O que **aumenta** de importância na era da IA:
- **Especificar bem o problema.** A IA é tão boa quanto o enunciado que você dá. Saber
  decompor o problema, definir critérios de sucesso e restrições é a habilidade central.
- **Julgar qualidade.** A IA produz código plausível, não necessariamente correto, seguro
  ou bem arquitetado. Quem não sabe avaliar não sabe quando a saída está errada.
- **Arquitetura e fronteiras.** Decidir estrutura, contratos e onde as coisas vivem
  continua sendo trabalho humano — e é o que mantém um sistema gerado por IA coeso.
- **Integração e contexto.** Encaixar a peça gerada no sistema existente, com seus padrões
  e restrições, é onde a IA sozinha falha.

O que **diminui:** memorizar sintaxe, escrever boilerplate, lembrar a assinatura exata de
uma API. Delegue isso.

A virada de mentalidade: você deixa de ser *quem digita o código* para ser *quem dirige,
revisa e responde pela engenharia*. A responsabilidade pelo resultado continua sua.

---

## Usar IA bem em cada etapa

De *Programação Utilizando IA* e *IA Generativa para Desenvolvimento de Software* — a IA
ajuda no ciclo inteiro, não só na digitação:

- **Planejamento.** Use a IA pra explorar abordagens, levantar trade-offs, esboçar
  arquitetura e listar casos de borda que você esqueceria. Ótima parceira de brainstorm —
  mas a decisão é sua.
- **Programação.** Geração de funções, refatoração, tradução entre linguagens, explicação
  de código legado. Dê contexto rico (o padrão do projeto, as restrições) e itere; prompts
  vagos geram código genérico.
- **Testes.** A IA é excelente pra gerar casos de teste, inclusive de borda, e pra propor
  dados de teste. Mas peça que os testes verifiquem **comportamento**, e confira se não são
  testes que só repetem a implementação.
- **Depuração.** Cole o erro completo e o contexto; a IA ajuda a formar hipóteses. Ainda
  assim, valide a causa raiz você mesmo — ela pode "alucinar" uma explicação plausível e
  errada.
- **Documentação e revisão.** Gerar rascunhos de docs, mensagens de commit, descrições de
  PR e primeira passada de revisão. Você edita e assume.

Princípio: **a IA acelera as etapas; ela não dispensa o entendimento.** Quanto mais você
entende, mais valor extrai dela — e menos cai nas armadilhas dela.

---

## Revisar e confiar (com verificação) na saída da IA

Riscos concretos do código gerado, e como mitigá-los:

- **Alucinação e plausibilidade.** Código que *parece* certo mas chama API inexistente,
  trata o caso errado ou tem off-by-one. → Rode, teste, leia de verdade. Nunca declare
  pronto sem evidência de execução.
- **Segurança.** A IA frequentemente reproduz padrões inseguros (injeção, segredos no
  código, validação ausente). → Revise com olhar de segurança; valide entradas; use
  consultas parametrizadas.
- **Licenciamento e dados sensíveis.** Atenção ao que entra no prompt (segredos, código
  proprietário) e à proveniência do que sai.
- **Erosão de entendimento.** Aceitar sem entender cria um sistema que ninguém compreende —
  dívida técnica que cobra juros na primeira manutenção. → Só faça merge do que você
  consegue explicar.
- **Viés do "quase certo".** O custo escondido é o tempo gasto consertando código 90%
  pronto. Às vezes especificar melhor e regenerar é mais barato que remendar.

Mentalidade: trate a IA como um par júnior brilhante e veloz — gera muito, mas **você** é
o revisor sênior responsável.

---

## Mentalidade de produto: construir a coisa certa

De *O Engenheiro de Software com Mentalidade de Produto* — a diferença entre escrever
código e gerar impacto:

- **Comece pelo problema do usuário, não pela solução.** A pergunta antes de "como
  construo?" é "isso resolve uma dor real e é a prioridade certa agora?". Muito esforço de
  engenharia é desperdiçado construindo bem a coisa errada.
- **Entenda o porquê.** Engenheiros com mentalidade de produto conhecem as metas de
  negócio e do usuário, e usam esse contexto pra tomar decisões melhores no dia a dia (o
  que cortar, o que simplificar, onde investir qualidade).
- **Entregue valor em incrementos.** Fatias finas que chegam ao usuário e geram aprendizado
  valem mais que a "solução completa" que demora e pode estar errada.
- **Diga não com critério.** Saber o que **não** construir — features especulativas,
  generalização prematura — é tão valioso quanto construir.
- **Pense em todo o ciclo de vida.** Custo de operação, manutenção, observabilidade e
  experiência do usuário fazem parte do "pronto". Código que ninguém consegue operar não
  está pronto.
- **Comunique e colabore.** Influência, clareza ao escrever e ao alinhar com produto/design
  multiplicam o impacto técnico.

---

## O novo perfil do desenvolvedor

Juntando as quatro obras, o desenvolvedor que prospera na era da IA:

1. **Domina os fundamentos** (esta é a base que separa quem julga a IA de quem só copia) —
   ver `references/01-fundamentos-e-craft.md` e `references/02-arquitetura-e-sistemas.md`.
2. **Especifica e decompõe problemas** com clareza, porque isso comanda tanto a IA quanto
   a equipe.
3. **Usa IA como alavanca** em todas as etapas, sem terceirizar o entendimento nem a
   responsabilidade.
4. **Pensa como produto** — otimiza para impacto no usuário, não para volume de código.
5. **Verifica antes de afirmar** — evidência de execução, não "deveria funcionar".

A IA não substitui o engenheiro; ela aumenta a distância entre quem só programava e quem
faz engenharia de software.

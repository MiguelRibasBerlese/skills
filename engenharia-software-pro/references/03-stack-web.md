# Stack Web e Dados

Síntese de: *Padrões JavaScript*, *Aprendendo TypeScript*, *React Fluente*, *Aprendendo
Node*, *O Guia do Mochileiro Python* e *SQL Guia Prático*.

## Índice
- JavaScript: padrões e armadilhas
- TypeScript: tipos a serviço da clareza
- React: pensar em UI declarativa
- Node: I/O assíncrono no servidor
- Python: práticas idiomáticas
- SQL: pensar em conjuntos

---

## JavaScript: padrões e armadilhas

*Padrões JavaScript* trata a linguagem como ela é — flexível e cheia de armadilhas — e
ensina a domá-la:

- **Escopo, `this` e closures** são a base de quase todo bug e quase todo padrão. Closures
  capturam variáveis por referência; `this` depende de *como* a função é chamada, não de
  onde foi definida (arrow functions herdam o `this` léxico — use-as para callbacks).
- **Prefira const, evite estado global.** Variáveis globais são acoplamento implícito.
  Encapsule com módulos.
- **Padrões úteis:** módulo (encapsular privado/público), fábrica (criar objetos sem expor
  construção), observador (eventos/assinaturas), e composição sobre herança profunda
  (cadeias de protótipo longas são frágeis).
- **Assíncrono:** `Promise` e `async/await` substituem o "callback hell". Trate erros
  (`try/catch` em `async`, `.catch` em promises) — promise rejeitada e ignorada é bug
  silencioso.
- **Igualdade e coerção:** use `===`; entenda valores *falsy* (`0`, `""`, `null`,
  `undefined`, `NaN`). Boa parte dos bugs "misteriosos" é coerção implícita.
- **Imutabilidade prática:** espalhe (`{...obj}`, `[...arr]`) em vez de mutar; combina com
  React e reduz bugs de estado compartilhado.

---

## TypeScript: tipos a serviço da clareza

TS não é "JS com burocracia" — é uma ferramenta para tornar o **contrato** do código
explícito e pegar erros antes de rodar. De *Aprendendo TypeScript*:

- **O sistema de tipos é estrutural** ("duck typing"): se tem o formato certo, serve. Pense
  em tipos como descrição da forma dos dados, não como classes rígidas.
- **Deixe o TS inferir.** Não anote o que ele já sabe; anote fronteiras (parâmetros de
  função, retornos públicos, dados externos). Tipo redundante é ruído.
- **Union e narrowing** modelam a realidade: um valor que é "ou A ou B". O compilador te
  obriga a tratar cada caso (`if`/`switch` com *type guards*) — isso elimina classes de bug.
- **`unknown` em vez de `any`.** `any` desliga o compilador; `unknown` força você a checar
  antes de usar. Use `any` só como último recurso e marque a dívida.
- **Generics** dão reutilização com segurança de tipo (uma função/coleção que funciona pra
  qualquer T preservando o tipo). Não exagere — generic complexo demais piora a leitura.
- **Tipos utilitários** (`Partial`, `Pick`, `Omit`, `Record`) derivam tipos uns dos outros,
  mantendo uma única fonte de verdade.

A mentalidade: deixe os tipos refletirem o domínio. Se um estado é impossível, torne-o
*irrepresentável* — assim o compilador impede o bug.

---

## React: pensar em UI declarativa

*React Fluente* — a mudança mental é **declarar a UI como função do estado**, não manipular
o DOM passo a passo:

- **UI = f(estado).** Você descreve como a tela *deve parecer* dado o estado; o React
  reconcilia o DOM. Pare de pensar "quando clicar, mude tal elemento" e pense "qual estado
  esse clique altera".
- **Componentes pequenos e compostos.** Um componente, uma responsabilidade. Componha em
  vez de criar megacomponentes com dezenas de props.
- **Estado mínimo e bem localizado.** Guarde o mínimo de estado e *derive* o resto. Estado
  duplicado é fonte de inconsistência. Suba o estado só até o ancestral comum que precisa
  dele.
- **Hooks com disciplina.** `useState` para estado local; `useEffect` *apenas* para
  sincronizar com sistemas externos (rede, DOM, timers) — não para lógica que poderia ser
  derivada na renderização. Efeito mal-usado é a maior fonte de bug e re-render em excesso.
  Respeite o array de dependências (ele não é decoração).
- **Listas precisam de `key` estável** (não use índice se a lista reordena).
- **Performance só quando medida.** `memo`, `useMemo`, `useCallback` resolvem problemas
  reais de re-render — aplicados sem medição, só adicionam complexidade. Meça primeiro.
- **Imutabilidade é obrigatória** no estado: nunca mute; produza novos objetos/arrays.

---

## Node: I/O assíncrono no servidor

*Aprendendo Node* — JS no servidor, com um modelo próprio:

- **Event loop e não-bloqueio.** Node é single-thread para o seu código; ele brilha em I/O
  concorrente (rede, arquivo, banco). **Nunca bloqueie o loop** com trabalho de CPU pesado
  síncrono — isso trava *todas* as requisições. Para CPU intensiva, use worker threads ou
  outro serviço.
- **Tudo é assíncrono e baseado em eventos.** Domine `async/await`, streams (processar
  dados aos pedaços sem carregar tudo na memória) e `EventEmitter`.
- **Trate erros sempre.** Erro não capturado em assíncrono pode derrubar o processo.
  `try/catch` em `async`, middleware de erro no Express, e nunca engula rejeições.
- **Módulos e dependências.** O ecossistema npm é enorme — escolha dependências com critério
  (manutenção, segurança, tamanho); cada dependência é superfície de risco.
- **Configuração e segredos fora do código** (variáveis de ambiente), e valide a entrada
  na fronteira da API.

A força do Node é compartilhar mentalidade e código entre cliente e servidor; a armadilha
é tratar trabalho de CPU como se fosse I/O.

---

## Python: práticas idiomáticas

*O Guia do Mochileiro Python* é sobre **como um pythonista profissional trabalha**, não
sintaxe:

- **Código pythônico ("The Zen of Python").** Explícito melhor que implícito; simples
  melhor que complexo; legibilidade conta. Há geralmente "um jeito óbvio de fazer".
- **Estrutura de projeto e ambientes.** Use ambientes virtuais (`venv`) e fixe dependências;
  jamais instale tudo no Python do sistema. Estruture o projeto de forma previsível (módulos,
  `pyproject`/requirements, testes separados).
- **Idiomas que importam:** compreensões de lista/dict (declarativas), gerenciadores de
  contexto (`with` — garante limpeza de recursos), geradores (`yield` — processar grandes
  volumes sem estourar memória), e desempacotamento.
- **Estilo e ferramentas.** Siga PEP 8; use formatadores e linters (a discussão de estilo é
  resolvida pela ferramenta, não no PR). Type hints melhoram clareza em bases grandes.
- **Trate exceções com precisão.** Capture exceções específicas, não `except:` genérico que
  esconde bugs.
- **Teste e empacote.** `pytest` para testes; entenda como distribuir o que você cria.

---

## SQL: pensar em conjuntos

*SQL Guia Prático* — a virada mental é **declarar o resultado**, não iterar linha a linha:

- **Pense em conjuntos.** Você descreve *quais* dados quer; o banco decide *como* obtê-los.
  Resista a transformar SQL em laço imperativo (cursores) quando uma consulta declarativa
  resolve.
- **JOINs são o coração.** Entenda INNER (interseção), LEFT (tudo da esquerda + casamentos),
  e quando cada um se aplica. Erro de JOIN é a fonte nº 1 de resultados errados (duplicação
  ou perda de linhas).
- **Agregação e GROUP BY.** `COUNT`, `SUM`, `AVG` com agrupamento; `HAVING` filtra grupos
  (≠ `WHERE`, que filtra linhas antes de agrupar).
- **Índices: a alavanca de desempenho.** Um índice transforma uma varredura completa O(n)
  numa busca rápida — mas custa escrita e espaço. Indexe colunas usadas em filtros e JOINs;
  não indexe tudo.
- **Normalização vs. desnormalização.** Normalize para integridade (uma verdade, sem
  redundância); desnormalize conscientemente quando leitura precisa de velocidade. É
  trade-off, como tudo.
- **Transações e integridade.** ACID, chaves estrangeiras e restrições protegem os dados de
  estados inválidos — deixe o banco fazer esse trabalho em vez de confiar só na aplicação.
- **Cuidado com injeção de SQL:** sempre use *consultas parametrizadas*, nunca concatene
  entrada do usuário na query.

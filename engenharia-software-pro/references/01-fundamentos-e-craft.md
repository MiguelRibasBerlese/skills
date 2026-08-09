# Fundamentos e Ofício

Síntese de: *Entendendo Algoritmos*, *Entendendo Estruturas de Dados*, *Aprenda
Programação Funcional*, *O Programador Pragmático (2ed)*, *Programador Autodidata*, *Como
Ser Um Programador Melhor* e *Desenvolvimento Real de Software (fundamentos em Java)*.

## Índice
- Algoritmos: como pensar sobre custo
- Estruturas de dados: escolher a certa
- Programação funcional: pensar em transformações
- O ofício pragmático
- Carreira e aprendizado autodidata
- Desenvolvimento real: do exercício ao projeto

---

## Algoritmos: como pensar sobre custo

O valor prático de algoritmos não é decorar implementações — é **estimar custo** e
**reconhecer padrões de solução**.

**Notação Big-O é sobre crescimento, não sobre velocidade absoluta.** Ela responde "se a
entrada dobrar, quanto piora?". O(1) ignora o tamanho; O(log n) mal sente; O(n) acompanha;
O(n log n) é o teto saudável pra ordenação; O(n²) começa a doer; O(2ⁿ) e O(n!) só servem
pra entradas minúsculas. Antes de otimizar, pergunte: o gargalo é o algoritmo ou o I/O?
Frequentemente é I/O, e trocar O(n²) por O(n) num laço que roda 50 vezes não muda nada.

**Padrões que resolvem a maioria dos problemas:**
- *Busca binária* — em dados ordenados, corte o espaço pela metade a cada passo (O(log n)).
- *Dividir e conquistar* — quebre em subproblemas iguais menores (merge sort, quicksort).
- *Tabelas hash* — troca memória por tempo: busca/inserção O(1) médio. A primeira coisa a
  considerar quando você precisa de "achar rápido por chave".
- *Busca em grafos* — BFS acha o caminho com menos arestas; DFS explora fundo. Modele o
  problema como nós e arestas e metade da batalha está vencida.
- *Programação dinâmica* — quando subproblemas se repetem, memorize resultados. O salto
  mental é enxergar o problema como uma grade de subproblemas.
- *Algoritmos gulosos* — escolha o ótimo local a cada passo; nem sempre dá o ótimo global,
  mas quando dá, é simples e rápido.

A lição maior: **não reinvente**. Reconhecer "isso é um problema de caminho mínimo" vale
mais que escrever Dijkstra de cabeça.

---

## Estruturas de dados: escolher a certa

A pergunta-chave é **como os dados serão usados**, não como são guardados.

- *Array / lista contígua* — acesso por índice O(1), mas inserir no meio é caro. Ótimo
  quando você lê muito por posição e o tamanho é estável.
- *Lista ligada* — inserir/remover nas pontas é barato, mas não há acesso aleatório. Use
  quando a coleção muda muito e você raramente busca por índice.
- *Pilha (LIFO)* — desfazer, recursão, avaliação de expressões.
- *Fila (FIFO)* — tarefas em ordem de chegada, BFS, buffers.
- *Tabela hash / dicionário* — associação chave→valor com busca O(1) média. O cavalo de
  batalha do dia a dia.
- *Árvore (incl. BST, heap)* — hierarquia e ordem. Heap dá o mínimo/máximo em O(log n)
  (filas de prioridade). Árvores balanceadas mantêm busca ordenada eficiente.
- *Grafo* — relações n-para-n (redes, dependências, rotas).

Heurística: se você se pegar varrendo uma lista inteira repetidamente pra achar coisas,
provavelmente a estrutura está errada — um hash ou uma árvore resolve.

---

## Programação funcional: pensar em transformações

FP não é uma linguagem — é uma forma de modelar problemas como **transformações de dados**
em vez de sequências de comandos que mutam estado.

**Conceitos que mudam seu código mesmo em linguagens não-funcionais:**
- *Funções puras* — mesma entrada, mesma saída, sem efeito colateral. São triviais de
  testar e de raciocinar porque não dependem de nada externo.
- *Imutabilidade* — em vez de mudar um objeto, produza um novo. Elimina classes inteiras de
  bug de estado compartilhado e concorrência.
- *Funções de ordem superior* — `map`, `filter`, `reduce` substituem laços imperativos por
  intenção declarada: "transforme cada", "mantenha os que", "combine em um".
- *Composição* — encadeie funções pequenas em vez de uma função grande. Cada peça é
  testável isoladamente.
- *Tratar efeitos nas bordas* — mantenha o núcleo puro e empurre I/O/rede/banco pra
  periferia. Isso torna o miolo do sistema previsível.

Você não precisa converter tudo. O ganho prático: pegue uma função cheia de variáveis
mutáveis e laços aninhados e reescreva como uma pipeline de transformações — quase sempre
fica mais curta e mais clara.

---

## O ofício pragmático

Destilado do *Programador Pragmático* — a mentalidade, não a sintaxe:

- **Não deixe janelas quebradas.** Pequenas degradações ("depois eu arrumo") sinalizam que
  desleixo é aceitável e o código apodrece. Conserte ou marque explicitamente como dívida.
- **DRY — Don't Repeat Yourself.** Cada pedaço de conhecimento tem uma única fonte de
  verdade. Duplicação de conhecimento (não de texto) é o inimigo.
- **Ortogonalidade.** Componentes independentes: mudar um não deve quebrar outro. Reduz o
  raio de explosão de qualquer mudança.
- **Programe por contrato e falhe cedo.** Defina pré/pós-condições; valide na entrada;
  prefira um *crash* honesto a continuar com estado corrompido.
- **Automatize tudo que repete.** Build, testes, deploy, formatação. O que é manual é
  esquecido e errado.
- **Conhecimento como portfólio.** Aprenda uma linguagem nova por ano, leia, experimente.
  Diversifique pra não ficar preso a uma tecnologia.
- **Comunique.** Código é comunicação com humanos; o mesmo vale pra commits, PRs e docs.

---

## Carreira e aprendizado autodidata

Convergência entre *Programador Autodidata* e *Como Ser Um Programador Melhor*:

- **Fundamentos primeiro.** Linguagens e frameworks passam; algoritmos, estruturas de
  dados, redes, sistemas e versionamento ficam. Quem tem base aprende o novo rápido.
- **Aprenda fazendo e ensinando.** Projetos reais ensinam o que tutoriais não ensinam
  (debugging, integração, escopo). Explicar pra outra pessoa expõe os buracos do seu
  entendimento.
- **Leia código alheio.** Bons repositórios são livros-texto vivos. Você absorve padrões e
  estilo melhor do que em qualquer curso.
- **Desenvolva o hábito de depurar com método** (ver princípio de causa raiz no SKILL.md):
  reproduzir, isolar, hipótese, uma mudança por vez.
- **Soft skills contam.** Estimar, comunicar incertezas, pedir ajuda cedo, escrever bem —
  tudo isso decide carreira tanto quanto código.
- **Evite o culto à ferramenta nova.** Dominar o que você já usa rende mais que migrar pra
  o framework da moda toda semana.

---

## Desenvolvimento real: do exercício ao projeto

De *Desenvolvimento Real de Software* — a ponte entre "sei a sintaxe" e "construo
sistemas":

- **Exercícios isolados não preparam pra projetos.** O que diferencia é organizar código
  em módulos coesos, lidar com requisitos que mudam e manter o sistema testável conforme
  cresce.
- **Princípios SOLID como heurísticas, não mandamentos.** Responsabilidade única (uma razão
  pra mudar), aberto/fechado (estenda sem alterar), substituição de Liskov, segregação de
  interfaces, inversão de dependência. Use-os pra explicar *por que* um design dói, não pra
  decorar siglas.
- **Padrões de projeto são vocabulário.** Strategy, Observer, Factory, Decorator etc.
  existem pra nomear soluções recorrentes — aprenda o problema que cada um resolve, não só
  a estrutura. Aplicar padrão onde não há o problema é over-engineering.
- **Itere em vértices finos.** Construa uma fatia vertical completa (da entrada à saída) e
  evolua, em vez de construir todas as camadas pela metade.

# Arquitetura e Sistemas

Síntese de: *Fundamentos da Arquitetura de Software*, *Projetando Sistemas Distribuídos
(padrões com Kubernetes)*, *Aprenda Domain-Driven Design* e *Construindo Sistemas
Embarcados*.

## Índice
- O que é arquitetura (e o que ela troca)
- Atributos de qualidade dirigem o design
- Estilos arquiteturais e quando usar
- Sistemas distribuídos: padrões e falácias
- Padrões de contêiner (single-node e multi-node)
- Domain-Driven Design
- Sistemas embarcados: projetar sob restrição

---

## O que é arquitetura (e o que ela troca)

Arquitetura são as **decisões difíceis de reverter**: as fronteiras, os estilos e os
trade-offs estruturais que moldam tudo o que vem depois. A primeira lei: *tudo em
arquitetura é um trade-off*. Não existe "melhor arquitetura", existe a mais adequada às
restrições e aos atributos de qualidade que importam aqui.

O arquiteto não busca a solução certa — busca a **menos errada** para o contexto, e
documenta *por que* escolheu assim (registros de decisão / ADRs). Decisões sem o porquê
viram lendas que ninguém ousa mexer.

Evite o "Big Design Up Front" e a arquitetura especulativa. Decida no último momento
responsável: cedo o suficiente pra não pintar o sistema num canto, tarde o suficiente pra
ter informação real.

---

## Atributos de qualidade dirigem o design

Requisitos funcionais dizem *o que* o sistema faz; os **atributos de qualidade**
(requisitos não-funcionais) dizem *quão bem*, e são eles que ditam a arquitetura:

- *Escalabilidade* — aguenta mais carga? Horizontal (mais máquinas) costuma vencer vertical.
- *Disponibilidade / resiliência* — sobrevive a falhas parciais?
- *Desempenho / latência* — rápido o suficiente para o uso real?
- *Manutenibilidade / evolutibilidade* — fácil de mudar com segurança?
- *Segurança* — protege dados e acesso?
- *Observabilidade* — você consegue ver o que está acontecendo em produção?
- *Custo* — caro de operar?

Estes atributos competem entre si (mais consistência custa disponibilidade; mais
desempenho custa simplicidade). O trabalho do design é **priorizar explicitamente** os 3-5
que mais importam e aceitar conscientemente os demais.

---

## Estilos arquiteturais e quando usar

- **Monolito modular** — um deploy, módulos bem separados internamente. Subestimado: para a
  maioria dos sistemas que começam, é a escolha certa. Simples de operar, fácil de
  refatorar fronteiras enquanto você ainda está aprendendo o domínio.
- **Camadas (n-tier)** — apresentação / negócio / dados. Familiar, mas vira "monolito
  lama" se as camadas vazarem. Bom para CRUD direto.
- **Microsserviços** — serviços independentes, deploy independente. Compram autonomia de
  times e escala granular, ao **custo** enorme de complexidade distribuída (rede, dados
  espalhados, observabilidade). Não comece por aqui sem dor que justifique. "Você precisa
  ser deste tamanho para entrar nesse brinquedo."
- **Orientado a eventos** — componentes reagem a eventos assíncronos. Excelente
  desacoplamento e escala, mas raciocínio e depuração ficam mais difíceis (fluxo
  implícito).
- **Microkernel / plugins** — núcleo estável + extensões. Bom para produtos com muita
  customização.

Regra prática: **adie a distribuição até ela ser inevitável**. Migrar de monolito modular
bem-feito para serviços é tranquilo; voltar de microsserviços prematuros é doloroso.

---

## Sistemas distribuídos: padrões e falácias

As **falácias da computação distribuída** (assuma que todas são falsas): a rede é confiável;
a latência é zero; a banda é infinita; a rede é segura; a topologia não muda; há um único
administrador; o transporte é grátis; a rede é homogênea. Todo design distribuído precisa
lidar com falha parcial, timeout, reordenação e duplicação de mensagens.

**Consequências práticas:**
- *Teorema CAP* — sob partição de rede, escolha entre consistência e disponibilidade. A
  maioria dos sistemas web aceita consistência eventual para ganhar disponibilidade.
- *Idempotência* — operações devem poder ser repetidas sem efeito duplicado, porque
  retries vão acontecer.
- *Timeouts, retries com backoff e circuit breakers* — proteja-se da falha em cascata.
- *Observabilidade não é opcional* — logs estruturados, métricas e tracing distribuído são
  o que torna o sistema depurável.

---

## Padrões de contêiner (single-node e multi-node)

De *Projetando Sistemas Distribuídos* — padrões reutilizáveis para sistemas em contêineres
(pensados com Kubernetes, mas conceituais):

**Single-node (vários contêineres no mesmo pod):**
- *Sidecar* — um contêiner auxiliar acopla uma capacidade (logging, proxy, TLS) ao
  principal sem alterá-lo.
- *Ambassador* — um proxy local intermedia a comunicação com o mundo externo (sharding,
  retry), simplificando a aplicação.
- *Adapter* — padroniza a saída do contêiner principal (ex.: normaliza métricas) para um
  formato esperado por fora.

**Multi-node (coordenação entre máquinas):**
- *Replicado com balanceamento* — N réplicas iguais atrás de um balanceador para escala e
  disponibilidade.
- *Sharded* — particione os dados/carga por chave quando uma réplica não cabe tudo.
- *Scatter/gather* — distribua a consulta a vários nós e agregue as respostas.
- *Functions/event-driven (serverless)* — código efêmero acionado por eventos.
- *Batch (queue, coordinated)* — pipelines de trabalho em lote com filas e coordenação.

O valor desses padrões é serem **vocabulário compartilhado**: nomeie o padrão e o time
inteiro entende a estrutura.

---

## Domain-Driven Design

DDD alinha o software ao **negócio**, não à tecnologia. Síntese de *Aprenda DDD*:

**Estratégico (o mapa):**
- *Linguagem ubíqua* — um vocabulário único e preciso, compartilhado por devs e
  especialistas do domínio, refletido direto no código. Se o código fala "registro" e o
  negócio fala "apólice", há tradução perdendo informação.
- *Bounded contexts* — o mesmo termo significa coisas diferentes em partes diferentes do
  negócio ("conta" no contexto de cobrança ≠ no de login). Delimite contextos com
  fronteiras explícitas e modelos próprios; não force um modelo canônico universal.
- *Context mapping* — descreva como os contextos se relacionam (parceria, cliente/fornecedor,
  conformista, anticorrupção) para gerir dependências entre times.
- *Subdomínios* — separe o **core** (a vantagem competitiva, onde investir o melhor design)
  do *suporte* e do *genérico* (compre ou use pronto).

**Tático (os blocos):**
- *Entidades* (identidade ao longo do tempo) vs. *value objects* (definidos só pelos
  atributos, imutáveis).
- *Agregados* — agrupe entidades/VOs sob uma raiz que garante invariantes; transações não
  cruzam fronteiras de agregado.
- *Repositórios* — abstração de persistência por agregado.
- *Domain events* — fatos do negócio que aconteceram; ótimos para integrar contextos.

A maior lição do DDD é **estratégica**: gaste design onde o negócio se diferencia, e
mantenha o resto simples.

---

## Sistemas embarcados: projetar sob restrição

De *Construindo Sistemas Embarcados* — engenharia onde memória, energia, tempo e hardware
são escassos e o software roda "perto do metal":

- *Restrições viram requisitos de primeira classe* — orçamento de memória, consumo,
  determinismo temporal (sistemas de tempo real têm prazos que **não** podem estourar).
- *Padrões de projeto adaptados* — máquinas de estado para comportamento; camadas de
  abstração de hardware (HAL) para isolar o código do chip específico e permitir teste e
  portabilidade.
- *Concorrência e interrupções* — código que reage a eventos de hardware exige cuidado com
  reentrância, seções críticas e estado compartilhado (de novo: minimize estado mutável
  compartilhado).
- *Confiabilidade acima de tudo* — muitas vezes não há "reiniciar e tentar de novo". Falha
  segura, watchdogs e tratamento de erro previsível são centrais.
- *Teste é mais difícil e mais importante* — simule o hardware, teste no alvo, e desconfie
  de comportamento que "só funciona na minha bancada".

A mentalidade embarcada — pensar em custo de cada byte e cada ciclo — melhora também
código de servidor: ela te treina a enxergar desperdício que você normalmente ignora.

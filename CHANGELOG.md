# Changelog

> Evolução do template da pipeline. Não vai para o destino (`pipeline/guias/adocao.md`).

## v6

### Resumo

A v6 foi escrita do zero, com texto original, sobre o que a v5 já fazia bem: regras com motivo, legado que não se imita, posse fechada por arquivo, cinco níveis de implementador, conferência pelo diff, revisor independente, triagem de causa e evolução com autoridade definida. O que muda:

- o orquestrador age como tech lead: desenha na altura da arquitetura e entrega missões com objetivo, contexto, posse e contratos; o que a missão não fixa é do implementador;
- o carregamento é seletivo: cada papel lê o próprio contrato e só as áreas de conhecimento que os arquivos do trabalho acionam, e o orquestrador lê guias só por gatilho;
- a deriva tem mecanismo: precedente legítimo, sinal `legado`, `Anterior:` nos padrões, procedimento para mudança de convenção e inventário de legado na adoção;
- o paralelismo despacha por dependência, sem barreira de onda, com contrato primeiro, agregadores de dono único e marcos;
- a consistência da própria pipeline ganha uma conferência escrita, em vez de depender de releitura livre;
- a adoção em projeto existente e a migração da v5 voltam a ter roteiro.

### Diagnóstico da v5

1. A ficha invertia a autonomia: "`Livre` é a única liberdade" e "simule a implementação" levavam o orquestrador a desenhar o interior das fichas, e os exemplares viravam especificação.
2. O carregamento crescia com o projeto, não com a tarefa: todo implementador e revisor lia `normas.md` inteiro; as fontes de referência moravam em `projeto.md`, um salto a mais; o `AGENTS.md`, lido por todos, trazia a seção inteira do implementador.
3. As convenções de `projeto.md` (idioma, kebab-case) não estavam na leitura do revisor.
4. Legado só era conhecido se alguém o listasse; mudança de convenção não tinha procedimento para inventariar o código antigo nem para tirar o exemplar velho de circulação.
5. O paralelismo esperava a onda inteira, obrigava o consumidor a esperar o produtor mesmo com contrato definido e empurrava para a onda seguinte qualquer missão que tocasse um arquivo agregador.
6. A consistência da documentação (referências, protegidos, regras `ask`) dependia de releitura manual.
7. A adoção em projeto existente, que a v3 cobria, tinha sumido.

### Estrutura

```text
AGENTS.md                      todo agente: papéis, leis, conflitos, glossário, mapa
CLAUDE.md                      @AGENTS.md
README.md                      o template, para pessoas
pipeline/
  README.md                    uso, estrutura, níveis e sinais de saúde, para pessoas
  papeis/                      orquestrador (núcleo), implementador, revisor
  guias/                       paralelismo, revisão, falhas, evolução, escrita, adoção
  conhecimento/                índice e áreas: código, interface, stack
  projeto.md                   fatos: adoção, idioma, checagens, rodar, paralelismo, protegidos, ambiente
  backlog.md                   achados, propostas, pendências
  ocorrencias/                 falhas da pipeline (era impactos/)
```

- Cada documento abre com `> Para: … · Leia quando: …`. O `Mapa` de `AGENTS.md` repete essas linhas: um agente acha o que ler sem conhecer a estrutura. A conferência de `guias/escrita.md` mantém os dois iguais.
- As áreas ficam fora do mapa e entram pelo índice, com gatilho mecânico. Assim, uma área nova não exige mexer no `AGENTS.md`.

### Decisões principais

#### Tech lead e missão

- A ficha vira missão: `Objetivo`, `Contexto`, `Posse`, `Contratos`, `Restrições`, `Aceite`, `Áreas`, `Referências` e `Retentativa`.
- Autonomia por padrão: o que a missão não fixa é do implementador, dentro das regras e dos padrões. A devolução tem lista fechada: escrever fora da posse, mudar contrato, decisão cara de desfazer, conflito entre fontes, ambiguidade que muda o resultado, arquivo da posse mudado por outro, falta de ferramenta ou capacidade.
  - Por quê: com `Livre` como única liberdade, o orquestrador precisava prever o interior de cada ficha, e o nível do implementador perdia o sentido.
  - Em `t0`, resultado com mais de uma leitura continua sendo devolução, como o "dúvida é bloqueio" da v5.
- O desenho do orquestrador fica na altura da arquitetura. O que ele imagina do interior de uma missão serve para achar perguntas, contratos e riscos, e não vai para a missão.
- Proibido na missão: código da solução e trecho de documentação como instrução. Exceção: contrato exato, texto ou valor que o pedido exige, com o motivo.
- `Quem decide o quê` dá a intervenção proporcional: interno à posse e primeira instância de padrão, o implementador; contrato e posse, o orquestrador; caro de desfazer e direção do produto, o humano.
- Correção descreve problema e evidência, não a solução; escolha razoável que o tech lead faria diferente não é retrabalho; devolução retoma a mesma instância com a resposta.
- O relato ganha `Integração` (necessidade aditiva em arquivo fora da posse, sem bloquear) e o sinal `legado`. O implementador relê o próprio diff contra as áreas e o aceite antes de relatar.
- Os níveis `t0` a `t4` continuam com os mesmos modelos e esforços, descritos agora pelo julgamento que cabe a cada um: execução, adaptação, solução local, estrutura, garantias.

#### Carregamento por papel

- Implementador: `AGENTS.md`, o próprio papel, o índice e as áreas que a posse aciona. A missão também lista as áreas, e o implementador confere pelos gatilhos e lê a união: são duas determinações independentes, e uma regra obrigatória não depende de um julgamento de relevância.
- Revisor: `AGENTS.md`, o próprio papel, o índice, as áreas que o diff aciona e `projeto.md` (`Checagens` e `Rodar`).
- Orquestrador: `AGENTS.md`, o núcleo, `projeto.md`, `backlog.md` e as áreas da tarefa; guias só por gatilho. Caminho leve: uma missão, sem risco e sem falha, não lê guia nenhum.

#### Conhecimento por área

- `normas.md`, `padroes.md` e `particularidades.md` viram áreas em `pipeline/conhecimento/`, cada uma com `Fontes`, `Regras`, `Padrões` e `Armadilhas`. As fontes de referência (tema, ambiente, aliases, manifesto) saem de `projeto.md` e vão para a área que as usa.
- COD-1 a COD-11 e UI-1 a UI-10 mantêm ID e sentido, com texto novo. COD-1 diz agora que a ordem de exibição ao usuário é significado lógico.
- As convenções de idioma e kebab-case viram regras: COD-12 (identificadores em inglês, documentação em português), COD-13 (kebab-case) e UI-11 (texto da interface em português). Isso fecha a brecha do revisor, que não lia as convenções.
- As escolhas de instalação de `stack.md` viram STK-1 a STK-3, para que o revisor possa citá-las.
- Área nova é aplicada e declarada; dividir uma área muda gatilhos e por isso é proposta.

#### Prevenção de deriva

- Precedência mantida (regras, pedido, fontes, padrões, código), com uma tabela curta de conflitos em `AGENTS.md`.
- Precedente legítimo é regra cumprida ou padrão registrado; código não registrado é evidência e é conferido contra as regras antes de ser imitado.
- Legado que o `Legado:` não lista vira sinal, e o orquestrador o acrescenta como manutenção.
- Padrão ganha `Anterior:`, a forma antiga que não se imita.
- Duas formas convivendo: o implementador usa a que cumpre as regras e sinaliza `lacuna`; o orquestrador registra a atual como padrão.
- Mudança de convenção aprovada: a regra muda, o código que passa a descumpri-la é inventariado em `Legado:`, os exemplares velhos viram `Anterior:`, e a migração fica opcional no backlog.
- Entrega parcial deixa o que falta em `backlog.md › Pendências`, para outra sessão retomar.

#### Paralelismo

- Posse exclusiva, com mapa antes de despachar, como na v5.
- Despacho por dependência, sem barreira de onda: uma missão parte quando as dependências dela foram aceitas; em lotes, se a ferramenta só permitir isso.
- Contrato primeiro: dependência só de interface não serializa. Quando o consumidor precisa do código para tipar, uma missão curta materializa o contrato antes.
- Agregadores têm dono único; as outras missões pedem em `Integração`, e o dono aplica tudo de uma vez.
- Marcos: o exemplar que outras missões replicam é aceito, e revisado se for arriscado, antes das réplicas.
- Checagens completas só com nenhuma missão em execução.
- Mantidos: instalação, lock e geração em série; `t4` e defeito de causa desconhecida sozinhos; o limite de `projeto.md`; divisão por responsabilidade contra paralelismo artificial.

#### Governança e evolução

- Mantidos: os gatilhos, a avaliação de impacto, "aplique e declare" × "proponha e aguarde", a definição verificável de aditiva sem conflito, o pedido explícito como aprovação, o formato de proposta e a triagem de causa (`implementação`, `missão`, `pipeline`, `indeterminada`) com recorrência em `ocorrencias/`.
- A gravidade do achado vira classe: `crítico` ou `consistência`.
  - Por quê: `desvio` chocava com o sinal `desvio de padrão` do implementador.
- A triagem de causa e a nova tentativa saem do núcleo para `guias/falhas.md`.
  - Por quê: só servem quando algo falha; fora do núcleo, o caminho leve carrega cerca de 3 KB a menos. É o único arquivo além dos previstos no plano da v6.

#### Conferência da pipeline

- `guias/escrita.md` ganha a seção `Conferência`, que o orquestrador faz antes de entregar qualquer mudança em `pipeline/`, `AGENTS.md`, `.claude/` ou `.codex/`: referências `arquivo › título`, caminhos citados, mapa contra cabeçalhos, índice contra áreas e IDs, protegidos contra regras `ask`, paridade dos agentes, títulos únicos e formato.
  - Por quê: a v5 dependia de releitura sem roteiro, e foi assim que referências e listas sincronizadas à mão divergiram.

### Decisões descartadas

- Verificador em código (`pipeline/verificar.mjs`): chegou a ser escrito, em Node e sem dependências, e o humano preferiu não ter código na pipeline. As mesmas verificações viraram a conferência manual de `guias/escrita.md`; o custo é que a consistência volta a depender de quem confere.
- Skills para os papéis: a invocação depende de julgamento do modelo, e o mesmo conteúdo precisaria existir duas vezes, para o Claude Code e para o Codex.
- Instruções aninhadas por pasta e hooks de bloqueio: dependem da ferramenta, e a pipeline precisa valer igual nas duas.
- Worktree por missão: a integração viraria merge, e recursos compartilhados (lock, banco, portas) continuariam colidindo.
- Revisores paralelos por área: perdem os problemas que atravessam áreas, como contrato entre camadas.

### O que não mudou

- Os níveis, os modelos e o esforço de cada um no Claude Code e no Codex, e a lista fechada de `tools`.
- O revisor sempre novo, o brief sem raciocínio, os dois ciclos e o crítico corrigido mesmo depois deles.
- A conferência pelo diff contra a linha de base, o escalonamento pela causa e a entrega parcial na terceira falha.
- Git direto na branch principal, commit só pelo orquestrador e memória de agente desligada.

### Nomes

| v5                                | v6                                  |
| --------------------------------- | ----------------------------------- |
| ficha                             | missão                              |
| `Arquivos` e artefatos permitidos | `Posse`                             |
| `Ler antes`                       | `Áreas` e `Referências`             |
| `Feito quando`                    | `Aceite`                            |
| `Fora`                            | `Restrições`                        |
| `Falha anterior`                  | `Retentativa`                       |
| retorno: `Status`, `Bloqueio`     | relato: `Estado`, `Devolução`       |
| `Registro`                        | `Sinais`                            |
| normas, padrões, particularidades | áreas de `conhecimento/`            |
| gravidade `desvio`                | classe `consistência`               |
| onda                              | despacho por dependência            |
| `impactos/`                       | `ocorrencias/`                      |
| `orquestracao.md`                 | `papeis/orquestrador.md` e `guias/` |

### Onde ficou cada parte da v5

- `AGENTS.md`: papéis, leis (checagens, protegidos, decisões caras, memória, git), precedência e legado continuam em `AGENTS.md`; a seção do implementador foi para `pipeline/papeis/implementador.md`.
- `orquestracao.md`:
  - papel, autonomia, registro das decisões, entender, decidir antes e cobertura → `papeis/orquestrador.md`, seções `Papel`, `Autonomia`, `1. Entenda` e `2. Desenhe`;
  - divisão e níveis → `3. Escreva as missões`;
  - ondas e donos → `guias/paralelismo.md`;
  - conferência, checagens e produto → `4. Despache` e `5. Confira e integre`;
  - revisão, ciclos e achados → `6. Revise` e `guias/revisao.md`;
  - causa dos achados, falhas e escalonamento → `guias/falhas.md`;
  - entrega e commit → `7. Entregue`.
- `ficha.md` → o modelo e os campos da missão, em `papeis/orquestrador.md`.
- `revisao.md` → `papeis/revisor.md`.
- `evolucao.md` → `guias/evolucao.md`; o destino de cada sinal ficou no núcleo do orquestrador, em `Sinais do relato`.
- `escrita.md` → `guias/escrita.md`, com os modelos de regra, padrão, armadilha, fonte, backlog e ocorrência.
- `adocao.md` → `guias/adocao.md`, que ganha projeto existente e migração da v5.
- `normas.md` → as regras de `conhecimento/codigo.md` e `conhecimento/interface.md`.
- `padroes.md` e `particularidades.md` → `Padrões` e `Armadilhas` de cada área.
- `stack.md` → `conhecimento/stack.md`: a tabela, sem mudança, e as escolhas de instalação em STK-1 a STK-3.
- `projeto.md` → `projeto.md`; as fontes de referência foram para as áreas, e as convenções para COD-12, COD-13, UI-11 e `projeto.md › Idioma`.
- `impactos/` → `ocorrencias/`.

### Migração de um projeto na v5

O roteiro está em `pipeline/guias/adocao.md`, na seção da migração: os registros do projeto continuam valendo, com os mesmos IDs, e muda só onde cada um mora.

### Validação

#### Consistência e formato

- Enquanto existiu, o verificador passou nas 11 checagens e acusou cada um dos 23 defeitos injetados em cópias do repositório, um por cópia. Entre eles, os três do plano: referência quebrada, ID duplicado e exemplar inexistente. Os demais: mapa diferente do cabeçalho, documento fora do mapa ou sem cabeçalho, área fora do índice, gatilho divergente, prefixo errado, `Legado:` e `Anterior:` inexistentes, caminho citado inexistente, protegido sem regra `ask` e regra sem protegido, regra de git sem par, agente sem par, descrição e instruções divergentes, TOML e JSON inválidos, `CLAUDE.md` sem o import, título repetido e ID citado inexistente.
- Depois da remoção do script, o estado final foi conferido com uma cópia dele fora do repositório, sem problemas.
- `npx prettier@3.6.2 --check .` passa.

#### Preservação

- Todos os IDs da v5 (COD-1 a COD-11, UI-1 a UI-10) existem na v6, com o mesmo sentido. Entram COD-12, COD-13, UI-11 e STK-1 a STK-3.
- Cada limite, campo e mecanismo da v5 tem lugar na v6 (`Onde ficou cada parte da v5`). A conferência achou três pontos que tinham ficado implícitos e os tornou explícitos no núcleo do orquestrador: onde criar caminho novo, arquivo protegido na posse e referência quando não há exemplar.

#### Orçamento de contexto

Bytes que cada papel carrega no template, nos cenários típicos:

| Cenário                                       | v5      | v6      | Δ    |
| --------------------------------------------- | ------- | ------- | ---- |
| Pergunta simples                              | 5,5 KB  | 6,4 KB  | +16% |
| Implementador, só código                      | 14,7 KB | 19,2 KB | +31% |
| Implementador, interface                      | 14,7 KB | 22,5 KB | +53% |
| Revisor, diff de interface                    | 18,7 KB | 24,0 KB | +28% |
| Orquestrador, caminho leve                    | 36,7 KB | 36,2 KB | −1%  |
| Orquestrador, várias missões e risco          | 40,6 KB | 44,1 KB | +9%  |
| Orquestrador, com falha e mudança na pipeline | 53,9 KB | 64,3 KB | +19% |

- No template, a v6 carrega mais para implementador e revisor. O papel próprio traz devolução, integração, sinais e relato, e o `AGENTS.md` ganhou glossário e mapa. Com só duas áreas de regras, uma missão de interface lê todas as regras, como na v5.
- A diferença está no crescimento. Na v5, cada regra, padrão ou armadilha nova entrava na leitura de todo implementador e revisor. Na v6, ela só entra na leitura das missões cuja posse aciona a área. Uma missão só de código passa a carregar menos que na v5 quando o projeto acumula mais de 4,5 KB de conhecimento em áreas que ela não aciona; uma missão de interface, a partir de 7,8 KB.
- Para baixar o custo fixo, a triagem de falhas saiu do núcleo do orquestrador e o `AGENTS.md` foi enxugado: de uma primeira versão com 7,2 KB e um núcleo com 19,4 KB para 6,4 KB e 16,3 KB.

#### Leitura a frio

Quatro subagentes novos, sem contexto desta conversa e sem editar nada, leram um projeto fictício já adotado. Ele tinha legado listado e não listado, um padrão com `Anterior:` e um agregador.

- **Orquestrador, pedido com várias partes** (lista com busca, cadastro e menu):
  - leu os guias pelos gatilhos certos e pulou os que não disparavam;
  - fez uma só rodada de perguntas, cada uma com opções e recomendação;
  - escreveu missões sem código de solução e com contratos fixados;
  - despachou por dependência, revisou o marco antes das réplicas e deu dono único ao agregador do menu.
- **`t2`, missão de interface:**
  - leu as áreas certas;
  - seguiu o exemplar do padrão, não o `Anterior:`;
  - derivou a lista filtrada sem estado (COD-9) e usou o `Input` do Base UI (UI-1);
  - sinalizou os legados que o `Legado:` não listava;
  - devolveu a missão quando o aceite pedia uma checagem que o projeto não tinha.
- **Revisor:** achou os seis defeitos plantados (COD-3, COD-9, UI-7, UI-10, UI-11 e a busca que diferenciava maiúsculas). Achou também um que não tinha sido plantado (UI-1) e listou o legado não registrado em `Fora do escopo:`.
- **`t0` com texto ambíguo, no Haiku:**
  - na primeira leitura, escolheu o texto sozinho: a regra do `t0` vinha logo abaixo de "Ambiguidade que não muda o resultado é sua";
  - a regra virou exceção explícita, com exemplos;
  - na segunda leitura, devolveu com a recomendação, como deve.
- Os atritos apontados viraram ajustes: o que fazer quando o projeto ainda não testa, campo ausente na missão, posse já autorizada, a ordem de funções em COD-1, STK-1 sem forçar biblioteca onde a plataforma basta, rodar checagens e dar veredito sem subir o produto, `Base:` com mais de um valor, quebra que já existia na base, definição de configuração protegida, regra `ask` de protegido novo, revisão antecipada de marco, cache como interseção de posse, despacho que espera checagens completas, fronteira entre `t2` e `t3`, e a regra antes de delegar que só duplicaria a tabela.

#### Cenários

| Cenário                       | Caminho na v6                                                | Guias lidos                |
| ----------------------------- | ------------------------------------------------------------ | -------------------------- |
| Passo leve                    | uma missão `t0`, conferência, entrega                        | nenhum                     |
| Tela nova                     | desenho, missões por responsabilidade, revisão               | paralelismo, revisão       |
| Primeiro formulário           | cobertura antes; padrão e revisão do marco depois            | evolução, escrita, revisão |
| "A partir de agora, sempre X" | o pedido é a aprovação; aplica e declara                     | evolução, escrita          |
| Regra conflitante             | devolução com sinal `conflito`; precedência ou pergunta      | evolução                   |
| Mudança de convenção          | regra, `Legado:` inventariado, `Anterior:`, backlog          | evolução, escrita          |
| Falha repetida                | causa; 2ª ocorrência é `pipeline`; 3ª falha, entrega parcial | falhas, evolução           |
| Adoção de projeto existente   | fatos, fontes, choques, legado, duas formas                  | adoção, evolução, escrita  |
| Migração da v5                | arquivos realocados, IDs mantidos, conferência               | adoção, escrita            |

## v5

### Resumo

A v5 mantém o núcleo da v4: normas com motivo, fichas com arquivos fechados, cinco níveis de implementador, ondas paralelas com arquivos disjuntos, conferência pelo diff e revisor independente. O que muda:

- o orquestrador pergunta menos e registra o que decidiu sozinho;
- os achados de revisão têm gravidade, escopo e causa, com limite de ciclos e backlog;
- a pipeline evolui de forma proativa, com regra clara sobre o que se aplica e o que se propõe;
- o paralelismo tem donos explícitos por arquivo, artefato e recurso;
- a escrita separa obrigação de liberdade, e regras compostas viraram itens.

### Estrutura

- A v5 substitui a v4 na raiz, com a mesma árvore: `AGENTS.md`, `CLAUDE.md`, `.claude/`, `.codex/` e `pipeline/`.
- `pipeline/` continua plana. Entram dois arquivos:
  - `evolucao.md`: quando a pipeline muda e com que autoridade;
  - `backlog.md`: achados fora do escopo, sobras não críticas da revisão, propostas pendentes e pendências adiadas.
  - Por quê: doze arquivos não pedem pastas. A autoridade de cada arquivo fica numa lista única, em `evolucao.md › Aplicar ou propor`.
  - Alternativa descartada: pastas por autoridade (`processo/`, `registros/`). Simplificaria os globs de permissão, mas alongaria cada citação de ficha e revisão.
- `escrita.md` continua separado de `evolucao.md`.
  - Por quê: `escrita.md` responde "como escrever" e serve também para fichas e briefs; `evolucao.md` responde "posso mudar isto?". São perguntas de momentos diferentes.

### Decisões principais

#### Autonomia do orquestrador

- Pergunta só em três casos: irreversível ou de alto impacto, ambiguidade que muda o resultado, informação que só o humano tem (`orquestracao.md › Autonomia`).
- Ambiguidade só é pergunta quando não há leitura claramente melhor e as leituras levam a entregas diferentes. Isso preserva o "há leitura razoável → decida" da v4.
- Toda decisão tomada sem perguntar, entre alternativas que o humano poderia ter escolhido diferente, é registrada com o motivo na entrega, no brief do revisor e no corpo do commit.
  - Por quê: a v4 dizia "se relevante, vira linha na entrega", sem critério de relevância e sem registro durável. O commit é o registro que dura sem criar um arquivo de histórico.
  - Alternativa descartada: um `decisoes.md`. Cresceria sem limite e duplicaria o `git log`; decisões que outras tarefas repetem já têm lugar em `padroes.md`.
- Instalar uma biblioteca de `stack.md` não pede autorização; dependência fora dela é pergunta.
  - Por quê: o humano já escolheu a stack. Na v4, qualquer dependência nova era pergunta, o que contrariava essa escolha.

#### Achados de revisão

- O revisor classifica a gravidade: `crítico` (critério, defeito, segurança, norma ou proteção) ou `desvio` (desvio arquitetural que nenhuma norma proíbe).
- O orquestrador faz a triagem da causa antes de corrigir: `implementação`, `ficha`, `pipeline` ou `indeterminada` (`orquestracao.md › Causa dos achados`).
  - Por quê o orquestrador: só ele vê ao mesmo tempo a ficha, as normas e o achado. O revisor não recebe a ficha, por desenho, e o implementador julgaria o próprio trabalho.
  - Por quê `ficha` como causa própria: sem ela, um erro do orquestrador na ficha seria lançado como erro do implementador (e subiria o nível à toa) ou como erro de norma (e mudaria uma norma que estava certa). A v4 já tratava a ficha ambígua como "não é falha"; a v5 só dá nome a isso.
  - Para usar a causa `implementação`, o orquestrador cita o trecho violado e onde o implementador o tinha. Isso evita culpar o implementador por padrão.
  - Alternativa descartada: um agente triador. Precisaria receber ficha, normas e achado, que o orquestrador já tem, e custaria mais uma instância por revisão.
- O revisor ganha o campo opcional `Pipeline:`, para apontar norma ambígua ou ausente. Ele lê as normas como um implementador as leria, sem o contexto da implementação, e por isso é o melhor detector de ambiguidade. Para o orquestrador, o campo é indício, não prova.
- A causa `indeterminada` é registrada em `impactos/`. A segunda ocorrência do mesmo tipo passa a ser `pipeline`.
  - Por quê: sem memória entre sessões, a recorrência só aparece se a primeira ocorrência estiver escrita.
- Limite de dois ciclos por tarefa: revisão completa e, se a correção foi crítica ou substancial, uma conferência só dos achados e das correções.
  - Crítico no que a tarefa mudou é sempre corrigido, inclusive depois do limite. Nesse caso, quem confirma a correção é o orquestrador, sem terceiro revisor.
  - Não crítico que sobra vai para o backlog.
  - Por quê: o limite fecha o loop; a exceção para crítico impede que ele vire desculpa para entregar defeito.
- Achado em código que a tarefa não tocou vai para o backlog e não bloqueia a entrega. Se for crítico, a entrega o leva como pergunta, com recomendação.
  - Por quê: corrigir código fora da mudança amplia o escopo, pode colidir com outras fichas e contraria a regra de legado ("não o corrija fora do escopo"). Leitura adotada: "críticos sempre são corrigidos" vale para o que a tarefa mudou.

#### Normas proativas

- A checagem de cobertura acontece antes de delegar (`orquestracao.md › Cobertura da pipeline`): dependência ainda não usada, primeiro artefato de um tipo, integração nova, ferramenta nova, área sem escolha fechada.
  - Por quê: norma escrita depois que os implementadores decidiram chega tarde.
- Uma biblioteca nova costuma pedir duas entradas: uma norma antes (fecha a escolha) e um padrão depois da primeira instância (registra a forma).
- Autoridade em duas listas fechadas (`evolucao.md › Aplicar ou propor`):
  - aplica e declara: norma nova aditiva e sem conflito, padrões, particularidades, backlog, fatos de `projeto.md`, manutenção de norma que não muda o que ela exige;
  - propõe e aguarda: alterar ou remover norma, norma nova com conflito, qualquer mudança de processo, de `stack.md` ou de definições de agente.
- "Aditiva e sem conflito" tem definição verificável: não contradiz nem restringe entrada existente, não escolhe entre formas que já convivem e não cria legado.
- Pedido explícito do humano para mudar uma norma já é a aprovação. Conflito implícito entre o pedido e uma norma é pergunta.
  - Por quê: a v4 deixava o orquestrador mudar qualquer norma "no mesmo trabalho e declarar". A v5 separa o que o humano pediu do que o orquestrador inferiu.
- `normas.md` sai da lista `ask` de `.claude/settings.json` e da lista de protegidos.
  - Por quê: com o gate, toda norma nova aditiva pediria confirmação, o que anula a autonomia que o princípio concede. A regra de autoridade em `evolucao.md` vale igual no Claude Code e no Codex, que não tem esse gate. A conferência do diff continua impedindo que um subagente escreva ali.
  - Alternativa descartada: manter o gate. É mais seguro contra uma alteração rotulada por engano como aditiva, mas transforma toda norma nova em pergunta.

#### Delegação e paralelismo

- O `t0` é definido pelos três fechamentos: entrada, saída e aceite. Localizar e listar ocorrências entra como exemplo de tarefa mecânica.
- Os níveis viram uma escada conferida em ordem; vale o menor nível que dá conta de todo o julgamento da ficha.
- Donos explícitos (`orquestracao.md › Donos`): a ficha é dona dos seus arquivos, artefatos e recursos exclusivos do disparo até a conferência. Ninguém mais escreve ali, nem o orquestrador. O mapa de donos é montado antes de cada onda.
- O implementador devolve bloqueio se um arquivo seu mudar sem que ele o tenha escrito: é o sinal de que a regra de donos foi violada.
- Alternativa descartada: um worktree por ficha. Isolaria as escritas, mas a integração viraria merge, e comandos que usam recursos compartilhados (lock, banco, portas) continuariam colidindo.

#### Escrita

- `escrita.md` abre com o princípio "clareza não é brevidade", com um exemplo, e com um vocabulário fixo: frase imperativa é obrigação, `Livre:` ou "pode" com condição é liberdade, `Por quê:` só quando não é óbvio.
- Regras compostas da v4 viraram itens, sem perder conteúdo. A precedência entre fontes virou lista numerada.
- O `Registro` do implementador ganhou rótulos (`lacuna`, `norma ambígua`, `norma conflitante`...) que alimentam a triagem e `evolucao.md`.
- Contradições da v4 resolvidas:
  - "faça a etapa você mesmo" × "não escreva código do produto";
  - "nenhum arquivo guarda histórico" × `impactos/`;
  - "não há segunda rodada" × "pergunte uma vez" no imprevisto.

### O que não mudou

- `normas.md`: as normas COD e UI, sem alteração.
- `stack.md`: a tabela de bibliotecas.
- Modelos e esforço de cada nível no Claude Code e no Codex, e a lista fechada de `tools`.
- Conferência pelo diff contra a linha de base, escalonamento por causa, terceira falha leva a entrega parcial.
- Git direto na branch principal, commit só pelo orquestrador, memória de agente desligada.

### Migração de um projeto na v4

- Substitua pelos da v5: `AGENTS.md`, `CLAUDE.md`, as definições em `.claude/agents/` e `.codex/agents/`, e `pipeline/orquestracao.md`, `ficha.md`, `revisao.md`, `escrita.md`, `adocao.md` e `stack.md`.
- Acrescente `pipeline/evolucao.md` e `pipeline/backlog.md`, este só com as seções.
- Mantenha os registros do projeto: `normas.md`, `padroes.md`, `particularidades.md` e `impactos/`.
- Em `projeto.md`, mantenha o conteúdo do projeto e mude só:
  - `Arquivos protegidos`: a lista explícita de `pipeline/` da v5, sem `normas.md` e com `evolucao.md`;
  - `Paralelismo`: tire a regra de falta de vagas, que foi para `orquestracao.md`.
- Em `.claude/settings.json`, junte às regras do projeto as mudanças da v5: sai `Edit(/pipeline/normas.md)`, entra `Edit(/pipeline/evolucao.md)`.

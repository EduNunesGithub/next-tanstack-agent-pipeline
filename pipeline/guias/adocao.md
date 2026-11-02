# Adoção

> Para: orquestrador · Leia quando: `projeto.md › Adoção` não diz `adotado`.

## Estados

- `template`: a pipeline sem aplicação. Quando o pedido cria a aplicação, siga `Template`.
- `projeto existente`: a pipeline copiada para um projeto que já tem código. Siga `Projeto existente` antes do primeiro pedido de produto.
- `migração da v5`: um projeto que usava a v5 passando para a v6. Siga `Migração da v5`.
- `adotado`: este guia não se aplica mais.

## Em toda adoção

- Ferramentas: confira a disponibilidade de cada uma e a confiança que ela exige para carregar as configurações do projeto, pela documentação oficial atual. Não altere configuração pessoal para simular essa confirmação.
- `projeto.md`: o template não antecipa caminhos de configuração, comandos nem código de integração. Registre só o que conferir no destino.
- Padrões, armadilhas, backlog e ocorrências do repositório do template não viram entradas do destino.
- `CHANGELOG.md` documenta a evolução do template: não vai para o destino. O `README.md` do template dá lugar ao da aplicação.
- No fim: o estado `adotado` em `projeto.md › Adoção`, a conferência de `guias/escrita.md › Conferência` e as checagens completas passando.

## Template

Quando o pedido cria a aplicação, planeje as missões por `papeis/orquestrador.md`:

1. Confira o destino, as ferramentas disponíveis e a existência de Git. Escolha o gerenciador de pacotes adequado ao ambiente, ou siga o já adotado. O pedido de criação autoriza preparar a stack e os complementos necessários.
2. Crie o manifesto e o lock do destino. Instale as bibliotecas de `conhecimento/stack.md` que o pedido usa e configure a aplicação pela documentação das versões escolhidas e pelas regras.
3. Configure o desenvolvimento, a produção e as checagens (`Checagens da aplicação`). Escreva o `README.md` da aplicação para pessoas: pré-requisitos, instalação, desenvolvimento, produção local, endereço e acessos de teste.
4. Ponha na posse da missão de instaladores e geradores os artefatos que eles escrevem. Preserve os arquivos de instrução dos agentes: use a opção do framework que impede a reescrita automática deles, quando houver, e confira a saída antes de integrar.
5. Rode as checagens, observe a aplicação e registre o que conferiu:
   - em `projeto.md`: checagens, como rodar, paralelismo, arquivos protegidos e ambiente;
   - nas `Fontes` das áreas: estilos globais e tema, módulo de ambiente, aliases, manifesto e lock.

Além disso:

- As decisões do produto novo (domínio, persistência, autenticação, integrações, identidade visual) vêm do pedido. A stack não transfere componentes, contratos nem decisões de produto de outra aplicação.
- Nível num projeto vazio: criar uma aplicação Next.js não vira `t4` por ser do zero. Com a stack definida, dependências e configurações de resultado determinado podem ser `t0`; a primeira página com lógica local, `t2`, e as que repetem a forma dela, `t1`; uma integração com contrato por projetar, `t3`; autenticação com regras de acesso complexas, `t4`.

### Checagens da aplicação

- Na entrega da aplicação: formato, lint, tipos e build configurados e passando.
- Testes unitários e de navegador quando o comportamento os exige, não só porque a ferramenta existe.
- Regra que uma ferramenta consegue verificar, e que não tem exceção decidida caso a caso, ganha uma checagem automática, citada no `Checagem:` dela. As demais ficam com a revisão.
- Em `projeto.md › Checagens`:
  - as completas, do orquestrador, e as com escopo, que entram no `Aceite` das missões, cada uma com os pré-requisitos;
  - os marcadores de supressão das ferramentas instaladas, distintos das diretivas que elas exigem ou geram.
- Arquivos protegidos: as configurações de checagens, framework, tipos, dependências e comandos, infraestrutura e dados, hooks e integração contínua, cada uma com a regra `ask` em `.claude/settings.json`.
- Recursos exclusivos e agregadores: instalação de dependências, diretório de build, portas, bancos e serviços que os testes reiniciam, e os arquivos que várias missões tocariam, em `projeto.md › Paralelismo`.

## Projeto existente

O código já existe e foi escrito sem estas regras. Antes do primeiro pedido de produto, faça o inventário, com missões de exploração `t0` em paralelo onde couber:

1. **Fatos.** Confira e registre em `projeto.md` as checagens (completas, com escopo e marcadores de supressão), como rodar, paralelismo (recursos exclusivos e agregadores), arquivos protegidos, com as regras `ask`, e ambiente. Siga `Checagens da aplicação` no que faltar.
2. **Fontes.** Localize o tema e os estilos globais, o módulo de ambiente, os aliases, os schemas, o manifesto e o lock, e registre nas `Fontes` das áreas.
3. **Convenções em choque.** Liste as regras que o projeto, de forma consistente, cumpre de outro jeito (outra biblioteca de ícones, outro idioma, outra organização de pastas). Para cada uma, pergunte ao humano na mesma rodada:
   - adotar a regra, e o código existente vira legado;
   - ou ajustar a regra ao projeto, com a proposta no formato de `guias/evolucao.md › Proposta`.
4. **Legado.** Para cada regra mantida, localize e liste o código que a descumpre; os caminhos vão para o `Legado:` da regra.
5. **Formas duplicadas.** Liste o que o projeto faz de duas formas, como dois clientes HTTP, dois jeitos de validar formulário ou duas organizações de pasta. Para cada uma, registre a atual como padrão, por `guias/evolucao.md › Duas formas`. Escolha que muda o produto, ou que nenhum critério decide, é pergunta na mesma rodada.
6. **Armadilhas** que o humano conhece ou que o inventário revelou: nas áreas.
7. **Migração** do legado não faz parte da adoção. Se o humano quiser, vira pendência em `backlog.md`.

- Por quê: sem o inventário, o legado só aparece quando alguém o imita, e a forma antiga continua sendo copiada.

## Migração da v5

Os registros do projeto continuam valendo; muda onde cada um mora.

- `normas.md` → as regras de `conhecimento/codigo.md` e de `conhecimento/interface.md`, com os mesmos IDs, `Checagem:` e `Legado:`. Norma que o projeto acrescentou vai para a área do assunto; se nenhuma serve, área nova (`guias/evolucao.md › Áreas`).
- `padroes.md` → os `Padrões` da área do assunto.
- `particularidades.md` → as `Armadilhas` da área do assunto.
- `projeto.md`:
  - `Fontes de referência` → as `Fontes` das áreas;
  - `Convenções` → COD-12, COD-13 e UI-11. Se o projeto tinha outra convenção, ajuste o texto da regra ao que já valia: é a mesma convenção, sem conflito;
  - o resto → as seções da v6 de `projeto.md`.
- `stack.md` → `conhecimento/stack.md`, com as mudanças que o projeto fez na tabela.
- `impactos/` → `ocorrencias/`, com os arquivos.
- `backlog.md` → mantido. No texto das entradas, ficha passa a ser missão e a gravidade `desvio` passa a ser a classe `consistência`.
- `orquestracao.md`, `ficha.md`, `revisao.md`, `evolucao.md`, `escrita.md` e `adocao.md` → substituídos por `papeis/` e `guias/`.
- `AGENTS.md` e as definições de agente → os da v6. `CLAUDE.md` não muda.
- `.claude/settings.json` → mantenha as regras próprias do projeto e troque as regras `ask` da v5 pelas que `projeto.md › Arquivos protegidos` exige na v6.

Depois: a conferência de `guias/escrita.md › Conferência`, as checagens completas e o estado `adotado`.

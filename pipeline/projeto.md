# Projeto

> Registro de como o projeto de destino se conecta à pipeline. Arquivo protegido: muda com autorização do pedido ou do humano.
> Aponte para as fontes reais; não copie seu conteúdo nem registre uma implementação presumida.

## Estado de adoção

- Estado inicial: template, sem aplicação instalada. As bibliotecas principais e a orientação de instalação estão em `stack.md`.
- Origem: Pipeline v4, derivada da pipeline usada no projeto de referência. Só as instruções e a stack foram exportadas.
- Ainda não confirmados: implementação, dependências instaladas, gerenciador de pacotes, branch principal, ferramentas e modelos disponíveis, dados de teste, acessos, integrações, CI e limites do ambiente.

O orquestrador atualiza este registro com os fatos conferidos no destino. Um pedido de criar a aplicação autoriza essa atualização e as configurações necessárias; mudanças de direção seguem `orquestracao.md`. Só registre como existente, instalado, disponível, confiável ou testado o que tiver sido conferido.

## Convenções

- Documentação e descrição dos commits: português do Brasil, em Conventional Commits.
- Identificadores no código: inglês.
- Nomes de arquivos e pastas do produto: kebab-case, respeitando os nomes exigidos pelas ferramentas.
- Textos da interface: português do Brasil.

## Fontes do projeto

`stack.md` orienta as bibliotecas; `normas.md` define os limites. A IA escolhe a estrutura e a integração conforme o pedido, o projeto existente e a documentação oficial pertinente às versões adotadas.

Após a implementação, registre os caminhos reais e a responsabilidade das fontes que existirem:

- dependências, requisitos de execução, comandos e instalação reproduzível;
- configuração do framework, tipos, aliases, lint e formato;
- estilos, tema e tipografia global;
- composição global da aplicação e integrações de interface;
- dados, validação, persistência e contratos;
- testes, seus ambientes e dados de apoio;
- hooks Git e integração contínua.

Atualmente, não há fontes de aplicação registradas. Atualize as referências quando a implementação mudar; nomes de arquivos, formatos e modos de configuração não são contratos do template.

## Checagens

Registre os comandos que estiverem configurados e tiverem sido conferidos no destino, seus pré-requisitos e o escopo que aceitam. Distinga checagens completas, executadas pelo orquestrador, das checagens com escopo que podem entrar em `Feito quando` de uma ficha.

- No template, confira os documentos, a sintaxe das configurações existentes, o formato e as referências da pipeline.
- Na entrega de uma aplicação, build, formato, lint e tipos precisam estar configurados e passar, com as etapas exigidas pelas versões e ferramentas adotadas.
- Unitários validam comportamento isolado; testes de navegador validam fluxos reais e riscos da interface. Configure e execute os que o comportamento e a tarefa exigirem.
- Quando houver Git, confira o estado e os diffs, inclusive arquivos novos e whitespace. Sem Git, compare os arquivos com uma cópia da base.
- Se houver commits da tarefa, confira suas mensagens pela convenção adotada.

Execute cada checagem quando seus pré-requisitos existirem; registre o que ainda não se aplica e por quê. Não crie testes só pela disponibilidade da ferramenta. Rode as suítes aplicáveis ao que mudou; ausência de testes, filtros vazios e opções que mascaram falhas não comprovam aceite.

Registre os marcadores de supressão reconhecidos pelas ferramentas instaladas, para conferir os diffs conforme `orquestracao.md`. Diferencie supressões de diretivas exigidas ou geradas pelas ferramentas.

## Paralelismo

- Limite por onda: até 10 fichas, reduzido à capacidade disponível na ferramenta ou conta. Falta de vagas divide a onda; não muda o nível das fichas.
- Identifique os arquivos compartilhados reais antes de dividir a tarefa: manifestos, locks, configuração, composição global e arquivos que agreguem vários módulos.
- Identifique também os recursos exclusivos: instalação de dependências, ativação de hooks, checagens completas, servidores na mesma porta e diretórios de saída compartilhados.

Registre os caminhos e recursos efetivamente usados quando forem conhecidos; os efeitos indiretos de comandos e geradores entram nesse levantamento.

## Rodar e observar o produto

Após a inicialização, registre os procedimentos conferidos de instalação reproduzível, desenvolvimento e produção local, com seus pré-requisitos. Registre o endereço efetivo do servidor e os acessos ou dados de teste necessários quando estiverem disponíveis.

Observe as rotas e os fluxos afetados pelo pedido, confira suas respostas e exercite o comportamento esperado. Não presuma comandos, portas, rotas, credenciais ou serviços.

Indisponibilidade de ferramenta, serviço ou credencial segue `orquestracao.md`.

## Arquivos protegidos

- Instruções e ferramentas de agente: `AGENTS.md`, `CLAUDE.md`, `.claude/` e `.codex/`.
- Instruções da pipeline: `pipeline/`, exceto `pipeline/padroes.md`.
- No destino: configurações que definem checagens, arquivos verificados, framework, tipos, dependências, comandos, hooks e integração contínua.

Ao criar ou adotar uma configuração protegida, registre seu caminho real aqui e inclua a regra correspondente em `.claude/settings.json` na mesma entrega, antes de delegar alterações posteriores. O template protege seus próprios arquivos; as proteções da aplicação acompanham a implementação efetivamente adotada.

## Ferramentas de agente

- `.claude/agents/` e `.codex/agents/`: níveis `t0` a `t4` e `revisor`; modelo e esforço em cada definição. Preserve o agente escolhido pela ficha; indisponibilidade real é declarada, sem substituição silenciosa. As definições, inclusive as edições, só valem numa sessão aberta depois da mudança.
- Ferramentas dos subagentes no Claude Code: lista fechada em `tools` de cada definição, só com o que o trabalho deles usa, porque cada ferramenta disponível pesa no contexto de todos os turnos. Se uma ficha precisar de outra (inclusive de MCP, como `mcp__<servidor>`), o orquestrador faz essa etapa ou a acrescenta à definição do nível, como mudança protegida.
- `.claude/settings.json`: memória automática desativada e regras de confirmação para alterações protegidas e comandos Git indicados.
- `.codex/config.toml`: memória automática desativada e limite configurado de subagentes. Permissões efetivas vêm da sessão; não equivalem às regras de confirmação do Claude Code.

No destino, confira a disponibilidade das ferramentas e a confiança necessária para carregar suas configurações locais conforme a documentação oficial atual. Não altere configurações pessoais para simular essa confirmação.

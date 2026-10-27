# Adoção

> Para o orquestrador, enquanto o estado de adoção em `projeto.md` for template: instalar a pipeline no destino e criar a aplicação.

## Instalar a pipeline no destino

- Ferramentas: confira a disponibilidade das ferramentas e a confiança necessária para carregar suas configurações locais conforme a documentação oficial atual. Não altere configurações pessoais para simular essa confirmação.
- `projeto.md`: o template não antecipa caminhos de configuração, comandos de execução nem código de integração da aplicação; registre só o que for conferido no destino.
- `padroes.md`, `particularidades.md`, `backlog.md` e `impactos/`: começam vazios; exemplares, armadilhas, pendências e lições da origem não viram entradas do novo projeto.
- `CHANGELOG.md`: documenta a evolução do template, não do projeto; remova-o do destino.

## Criar a aplicação

Quando o pedido criar a aplicação, planeje as fichas conforme `orquestracao.md`:

1. Confira o destino, as ferramentas disponíveis e a existência de Git. Escolha o gerenciador adequado ao ambiente ou siga o já adotado. O pedido de criação autoriza preparar a stack e seus complementos necessários.
2. Crie ou ajuste o manifesto e o lock próprios do destino. Instale as bibliotecas de `stack.md` que o pedido usa e configure a aplicação conforme a documentação das versões escolhidas e as normas.
3. Configure os procedimentos de desenvolvimento e de produção e as checagens (seção Checagens). Descreva em `README.md`, para pessoas, os pré-requisitos, a instalação, o desenvolvimento, a produção local, o endereço e os acessos de teste.
4. Delimite na ficha os efeitos de instaladores e geradores, incluindo os artefatos. Preserve os arquivos de instruções dos agentes; use a opção do framework que impeça sua reescrita automática, quando disponível, e confira a saída antes de integrar.
5. Rode as checagens aplicáveis ao estado integrado, observe a aplicação e registre em `projeto.md`, conforme `escrita.md`, o que foi conferido, inclusive o estado de adoção `adotado`.

Além disso:

- Decisões do novo projeto: domínio, persistência, autenticação, integrações e identidade visual, conforme o pedido. A stack não transfere componentes, contratos nem decisões de produto da aplicação de origem.
- Nível num projeto vazio: criar uma aplicação Next.js não vira uma ficha `t4` por ser "do zero". Com a stack definida, dependências e configurações de resultado determinado podem ser `t0`; uma página com lógica local, `t2`, e as seguintes que repetem a forma dela, `t1`. Uma integração com contrato ainda por projetar pode ser `t3`; autenticação com regras de acesso complexas, `t4`.

## Checagens

- Na entrega: formato, lint, tipos e build configurados e passando.
- Testes: unitários e de navegador quando o comportamento os exigir, não só porque a ferramenta existe.
- Normas: a que uma ferramenta consegue verificar e não tem exceção decidida caso a caso ganha uma checagem automática, citada no `Checagem:` dela; as demais ficam com a revisão.
- Em `projeto.md`: as completas (orquestrador) e as com escopo por arquivo (`Feito quando` das fichas), com seus pré-requisitos, e os marcadores de supressão das ferramentas instaladas, distintos das diretivas que elas exigem ou geram.

## Proteção e paralelismo

- Arquivos protegidos: as configurações de checagens, framework, tipos, dependências e comandos, infraestrutura e dados, hooks e integração contínua, registradas conforme `projeto.md › Arquivos protegidos`.
- Recursos exclusivos: instalação de dependências, diretório de build, portas e bancos ou serviços que os testes reiniciam, registrados em `projeto.md › Paralelismo`.

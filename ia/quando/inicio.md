# Início

`ia/fatos.md › Estado` ainda diz `modelo`.

- Já há código de aplicação no repositório: `Projeto existente`, antes do primeiro pedido de produto.
- Não há: `Projeto novo`, quando o pedido criar a aplicação.

## Sempre

- Registre em `ia/fatos.md` só o que conferir no destino. Nada presumido.
- Confira, pela documentação oficial atual, que cada ferramenta de agente carrega as configurações do projeto. Não altere configuração pessoal para simular isso.
- O `README.md` do modelo dá lugar ao da aplicação.
- Moldes, alertas, pendências e diário começam vazios no destino.
- No fim: checagens completas passando e `Estado` em `em uso`.

## Projeto novo

1. Confira o destino, as ferramentas e o Git. Gerenciador de pacotes: o já adotado, ou o adequado ao ambiente. O pedido de criação autoriza a stack e os complementos necessários.
2. Crie o manifesto e o lock. Instale as bibliotecas de `ia/regras/bibliotecas.md` que o pedido usa e configure pela documentação das versões escolhidas e pelas regras.
3. Configure desenvolvimento, produção e checagens (`Checagens da aplicação`). Escreva o `README.md` da aplicação, para pessoas: pré-requisitos, instalação, desenvolvimento, produção local, endereço e acessos de teste.
4. O que instaladores e geradores escrevem entra na raia. Preserve os arquivos de instrução dos agentes: use a opção do framework que impede a reescrita deles e confira a saída antes de integrar.
5. Rode as checagens, observe a aplicação e registre:
   - em `ia/fatos.md`: checagens, supressões, como rodar, paralelo;
   - no `Fonte:` das regras que o pedem: aliases, módulo de ambiente, tema ou estilos globais, manifesto e lock.

Além disso:

- As decisões do produto (domínio, persistência, autenticação, integrações, identidade visual) vêm do pedido. A tabela de bibliotecas não traz componentes, contratos nem decisões de outra aplicação.
- A encomenda que configura o projeto, nos passos 2 e 3, é `executor-5`, mesmo com resultado determinado.
  - Porque: ela fixa versões, checagens e convenções que toda tarefa seguinte herda; um erro ali se repete em cada uma.
- O código do produto segue `ia/fluxo.md › Nível`. Ex.: a primeira página com lógica local, 3; as que repetem a forma dela, 2; integração com contrato por projetar, 4; autenticação com regras de acesso complexas, 5.

### Checagens da aplicação

- Na entrega da aplicação: formato, lint, tipos e build configurados e passando.
- Testes unitários e de navegador quando o comportamento exige, não só porque a ferramenta existe.
- Regra que uma ferramenta verifica, sem exceção decidida caso a caso, ganha checagem automática, citada no `Garantia:` dela.
- Em `ia/fatos.md`:
  - as checagens completas e as com escopo, com os pré-requisitos;
  - os marcadores de supressão das ferramentas instaladas, distintos das diretivas que elas exigem ou geram;
  - recursos exclusivos (instalação, diretório de build, portas, bancos e serviços que os testes reiniciam) e agregadores.
- Protegidos: a configuração de checagens, framework, tipos, dependências e comandos, infraestrutura e dados, hooks e integração contínua. Cada caminho ganha `Edit(/<arquivo>)` ou `Edit(/<pasta>/**)` em `permissions.ask` de `.claude/settings.json`, antes de qualquer encomenda mexer nele.

## Projeto existente

O código foi escrito sem estas regras. Faça o inventário, com explorações `executor-1` em paralelo onde couber:

1. **Fatos.** Confira e registre `ia/fatos.md` inteiro, e os protegidos. No que faltar, siga `Checagens da aplicação`.
2. **Fontes.** Localize aliases, módulo de ambiente, tema ou estilos globais, manifesto e lock: vão para o `Fonte:` das regras que os pedem.
3. **Convenções em choque.** Liste as regras que o projeto cumpre, de forma consistente, de outro jeito (outra biblioteca de ícones, outro idioma, outra organização). Para cada uma, pergunte na mesma rodada:
   - adotar a regra, e o código existente vira dívida;
   - ou ajustar a regra ao projeto, com a proposta de `ia/quando/reparo.md › Só com o humano`.
4. **Dívida.** Para cada regra mantida, liste o código que a descumpre no `Dívida:` dela.
5. **Formas duplicadas.** O que o projeto faz de dois jeitos: `ia/quando/reparo.md › Duas formas`.
6. **Alertas** que o humano conhece ou que o inventário revelou: no assunto.
7. **Migração** da dívida não faz parte do início. Se o humano quiser, vira pendência.

Porque: sem inventário, a dívida só aparece quando alguém a imita.

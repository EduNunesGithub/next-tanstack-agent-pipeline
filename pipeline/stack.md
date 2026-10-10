# Stack de referência

> Bibliotecas principais para orientar a arquitetura. O template não fixa versões nem um manifesto de dependências; a implementação segue as normas, o pedido e a documentação oficial atual.

## Bibliotecas principais

| Uso                                  | Bibliotecas                                |
| ------------------------------------ | ------------------------------------------ |
| Aplicação                            | Next.js com App Router, React e TypeScript |
| Estilos                              | Tailwind CSS e Tailwind Merge              |
| Primitivos de interface              | Base UI                                    |
| Animações                            | Motion                                     |
| Ícones                               | Lucide React                               |
| Formulários e validação              | TanStack Form e Zod                        |
| Dados remotos e cache                | TanStack Query                             |
| Coleções e consultas reativas locais | TanStack DB                                |
| Estado reativo do cliente            | TanStack Store                             |
| Dados tabulares                      | TanStack Table                             |
| Gráficos                             | TanStack Charts                            |
| Controle de execução                 | TanStack Pacer                             |
| Cores e arquivos locais              | React Colorful e React Dropzone            |
| Qualidade estática e formato         | ESLint e Prettier                          |
| Testes unitários                     | Vitest e Testing Library                   |
| Testes de navegador                  | Playwright                                 |
| Hooks Git e commits                  | Husky e Commitlint                         |

As bibliotecas orientam as soluções para as necessidades que cobrem. A composição e a implementação dependem do projeto; sua presença nesta lista não exige criar funcionalidades que o pedido não incluiu. Instale e integre cada biblioteca quando ela for necessária ao escopo.

O template não antecipa caminhos de configuração, comandos de execução nem código de integração da aplicação.

## Escolhas de instalação

- Localize e consulte a documentação oficial atual das bibliotecas envolvidas, conferindo as instruções pertinentes à versão adotada.
- Em um projeto novo, escolha versões compatíveis entre si, com o runtime e com a necessidade do projeto, priorizando versões estáveis quando disponíveis. Em um projeto existente, parta das dependências instaladas; mudanças de versão acompanham a necessidade da tarefa e suas verificações.
- Plugins, adaptadores, integrações, definições de tipos e outras dependências de suporte são escolhidos conforme a documentação de instalação e as normas; não há uma lista fixa no template.
- O manifesto de dependências e o lock adotados no destino são as fontes das versões instaladas e da instalação reproduzível. Registre seus caminhos reais em `projeto.md`. Trocas de bibliotecas principais ou decisões que mudem a arquitetura seguem `orquestracao.md`.

## Inicialização

Quando o pedido criar a aplicação, o orquestrador planeja as fichas conforme `orquestracao.md`:

1. Confira o destino, as ferramentas disponíveis e a existência de Git. Escolha o gerenciador adequado ao ambiente ou siga o já adotado. O pedido de criação autoriza preparar a stack e seus complementos necessários.
2. Crie ou ajuste o manifesto e o lock próprios do destino. Instale as bibliotecas necessárias e configure a aplicação conforme a documentação das versões escolhidas e as normas.
3. Configure os procedimentos de desenvolvimento, produção e checagens que atendam aos critérios de `projeto.md`. Registre ali as fontes, os caminhos e os comandos efetivamente adotados e conferidos.
4. Delimite na ficha os efeitos de instaladores e geradores, incluindo os artefatos. Preserve os arquivos de instruções dos agentes; use a opção do framework que impeça sua reescrita automática, quando disponível, e confira a saída antes de integrar.
5. Rode as checagens aplicáveis ao estado integrado, observe a aplicação e atualize os fatos confirmados de `projeto.md`.

Domínio, persistência, autenticação, integrações e identidade visual são decisões do novo projeto, conforme o pedido. A stack não transfere componentes, contratos nem decisões de produto da aplicação de origem.

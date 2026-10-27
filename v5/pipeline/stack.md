# Stack de referência

> Bibliotecas principais para orientar a arquitetura, sem versões: as instaladas estão no manifesto do destino. A implementação segue as normas, o pedido e a documentação oficial atual.

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
| Banco de dados e ORM                 | PostgreSQL e Drizzle ORM                   |
| Autenticação e organizações          | Better Auth                                |
| Variáveis de ambiente                | T3 Env (`@t3-oss/env-nextjs`) com Zod      |
| E-mail transacional                  | Nodemailer (Mailpit no desenvolvimento)    |
| Ambientes locais e de preview        | Docker Compose                             |
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

## Escolhas de instalação

- Localize e consulte a documentação oficial atual das bibliotecas envolvidas, conferindo as instruções pertinentes à versão adotada.
- Em um projeto novo, escolha versões compatíveis entre si, com o runtime e com a necessidade do projeto, priorizando versões estáveis quando disponíveis. Em um projeto existente, parta das dependências instaladas; mudanças de versão acompanham a necessidade da tarefa e suas verificações.
- Plugins, adaptadores, integrações, definições de tipos e outras dependências de suporte são escolhidos conforme a documentação de instalação e as normas; não há uma lista fixa no template.
- O manifesto de dependências e o lock adotados no destino são as fontes das versões instaladas e da instalação reproduzível.
- Instalar uma biblioteca desta lista, ou um complemento que a documentação oficial dela exige, não pede autorização: o humano já escolheu a stack. A primeira instalação de cada uma passa pela cobertura da pipeline (`orquestracao.md › Cobertura da pipeline`).
- Dependência fora desta lista, troca de biblioteca principal ou decisão que mude a arquitetura é pergunta (`orquestracao.md › Autonomia`). Mudar esta lista segue `evolucao.md`.

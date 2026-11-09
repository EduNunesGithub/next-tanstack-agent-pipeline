# Bibliotecas

A escolha é do humano. A tabela diz que biblioteca resolve cada necessidade, sem versões e sem obrigar ninguém a criar o que o pedido não incluiu.

| Necessidade                          | Bibliotecas                                |
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
| Qualidade estática e formato         | ESLint, Perfectionist e Prettier           |
| Testes unitários                     | Vitest e Testing Library                   |
| Testes de navegador                  | Playwright                                 |
| Hooks Git e commits                  | Husky e Commitlint                         |

## Regras

### B1 · Uma biblioteca por necessidade

Necessidade que pede uma biblioteca usa a da tabela. Duas bibliotecas para a mesma necessidade é proibido.

- Porque: o humano já escolheu, e uma segunda biblioteca dobra o que se aprende, testa e atualiza.
- Como:
  - Antes de instalar, confira se o projeto, a tabela ou a plataforma já resolvem a necessidade.
  - O que a plataforma e o React resolvem sem esforço não pede biblioteca: a tabela não obriga a trocar `useState` ou `Array.filter` por uma biblioteca da mesma necessidade.
  - Instalar uma biblioteca da tabela, ou um complemento que a documentação oficial dela exige, não pede autorização.
  - O pacote da configuração de ESLint que a documentação oficial de uma tecnologia do projeto recomenda (`ia/regras/ferramentas.md › F5`) é complemento dela: também não pede autorização.
- Exceto: dependência fora da tabela, troca de biblioteca principal ou mudança de arquitetura, com a autorização de `AGENTS.md › Leis`, 3.

### B2 · Só quando o pedido precisa

Uma biblioteca da tabela entra no projeto só quando o escopo do pedido precisa dela.

- Porque: a tabela orienta escolhas; não é lista de instalação.

### B3 · Instalação pela documentação da versão

A instalação segue a documentação oficial da versão adotada, com versões compatíveis entre si e com o runtime.

- Porque: instrução de outra versão gera configuração que não funciona, ou que funciona por acaso.
- Como:
  - Consulte a documentação oficial atual da biblioteca, nas instruções da versão adotada.
  - Projeto novo: versões estáveis, quando houver, compatíveis entre si, com o runtime e com a necessidade.
  - Projeto existente: parta das versões instaladas. Mudar de versão só acompanha a necessidade da tarefa e as checagens dela.
  - Plugins, adaptadores, integrações e definições de tipos seguem a documentação de instalação. Não há lista fixa.
- Fonte: o manifesto de dependências e o lock. Registre os caminhos aqui quando existirem.

## Moldes

Nenhum.

## Alertas

Nenhum.

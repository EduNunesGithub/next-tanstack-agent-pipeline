# Stack

> Para: todos os papéis · Leia quando: instalar, atualizar ou remover uma dependência, ou importar um pacote que não está no manifesto de dependências.

## Fontes

- Nenhuma registrada. Entram aqui, conferidos no destino, o manifesto de dependências e o lock, que são a fonte das versões instaladas.

## Bibliotecas

A escolha da stack é do humano. A tabela diz que biblioteca resolve cada necessidade, sem versões e sem obrigar ninguém a criar o que o pedido não incluiu.

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

### STK-1: Necessidade que pede uma biblioteca usa a da tabela; duas bibliotecas para a mesma necessidade é proibido.

- Por quê: o humano já escolheu a stack, e uma segunda biblioteca dobra o que se aprende, testa e atualiza.
- Como:
  - Antes de instalar, confira se o projeto, a tabela ou a plataforma já resolvem a necessidade.
  - O que a plataforma e o React resolvem sem esforço não pede biblioteca: a tabela não obriga a trocar `useState` ou `Array.filter` por uma biblioteca da mesma necessidade.
  - Instalar uma biblioteca da tabela, ou um complemento que a documentação oficial dela exige, não pede autorização.
  - O pacote da configuração de ESLint que a documentação oficial de uma tecnologia do projeto recomenda (CFG-5) é complemento dela: instalá-lo também não pede autorização.
- Exceção: dependência fora da tabela, troca de biblioteca principal ou mudança de arquitetura, com a autorização de `AGENTS.md › Decisões caras de desfazer`.

### STK-2: Uma biblioteca da tabela entra no projeto só quando o escopo do pedido precisa dela.

- Por quê: a tabela orienta escolhas; não é lista de instalação.

### STK-3: A instalação segue a documentação oficial da versão adotada, com versões compatíveis entre si e com o runtime.

- Por quê: instrução de outra versão gera configuração que não funciona ou que funciona por acaso.
- Como:
  - Consulte a documentação oficial atual da biblioteca, nas instruções da versão adotada.
  - Projeto novo: escolha versões estáveis, quando houver, compatíveis entre si, com o runtime e com a necessidade.
  - Projeto existente: parta das versões instaladas; mudar de versão só acompanha a necessidade da tarefa e as checagens dela.
  - Plugins, adaptadores, integrações e definições de tipos seguem a documentação de instalação; não há lista fixa.
- Fonte: o manifesto e o lock, em `Fontes`.

## Padrões

- Nenhum registrado.

## Armadilhas

- Nenhuma registrada.

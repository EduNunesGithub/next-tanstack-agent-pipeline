# TanStack

Só o que as checagens não pegam. O resto vem da documentação da versão instalada (`ia/regras/bibliotecas.md › B3`).

## Regras

### T1 · Query só para dado vivo no cliente

O TanStack Query entra quando o dado muda depois da carga sem navegação: atualização periódica, invalidação depois de gravar, paginação incremental, atualização otimista. Fora disso, vale `ia/regras/next.md › N3`.

- Porque: dado que só se lê na carga não precisa de cache no cliente, e duas formas de ler o mesmo dado divergem.
- Como:
  - O dado inicial vem do servidor, por prefetch e hidratação. Nunca por busca ao montar.
  - No servidor, um `QueryClient` por requisição, nunca em escopo de módulo: o cache compartilhado vaza dado entre usuários.
  - Dado do Query não se copia para `useState` nem para store (`ia/regras/react.md › R4`).

### T2 · Chave e opções numa fábrica

Cada consulta é definida uma vez, com `queryOptions`, num módulo do recurso. `useQuery`, prefetch, invalidação e atualização do cache usam a fábrica. Chave escrita à mão fora dela é proibida.

- Porque: chave repetida diverge, e a invalidação deixa de achar a consulta sem erro nenhum.

### T3 · Um schema para o formulário e o servidor

O schema Zod que valida o formulário é o mesmo que a Server Action ou o Route Handler aplica à entrada.

- Porque: a validação do cliente é conforto e a do servidor é a garantia; com dois schemas, uma aceita o que a outra recusa.
- Como: o schema mora num módulo que os dois lados importam, sem `server-only`.

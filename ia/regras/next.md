# Next.js

Só o que as checagens e a configuração recomendada não pegam. O resto vem da documentação da versão instalada (`ia/regras/bibliotecas.md › B3`).

## Regras

### N1 · Servidor por padrão

Página, layout e componente são Server Components. `"use client"` fica só na menor unidade que usa estado, efeito, evento ou API do navegador; nunca em `page.tsx` nem em `layout.tsx`.

- Porque: a diretiva leva ao navegador o arquivo e tudo o que ele importa, e tira dele o acesso direto aos dados.
- Como: a parte interativa vira um componente filho; o conteúdo de servidor chega a ele por `children` ou por props.
- Exceto: arquivo que o framework exige como cliente, como `error.tsx`.

### N2 · Código de servidor marcado

Módulo que lê banco, sessão ou segredo importa `server-only`.

- Porque: sem a marca, um import vindo do cliente leva o código ao navegador em silêncio; com ela, o build falha.
- Como: o pacote `server-only` é complemento do Next.js e não pede autorização (`ia/regras/bibliotecas.md › B1`).
- Garantia: o build.

### N3 · Primeira leitura no servidor

O dado da primeira renderização é lido no Server Component, por chamada direta à função de acesso. Nunca por `fetch` a uma rota da própria aplicação, nem por busca em efeito ao montar.

- Porque: evita a cascata de requisições, o estado de carregamento à toa e um endpoint público a mais para proteger.
- Como: Route Handler existe só para quem consome de fora (webhook, integração) ou para a biblioteca que o exige.

### N4 · Toda entrada do servidor se defende

Cada Server Action e cada Route Handler valida a entrada com schema e confere a autorização dentro de si. Nunca confia na proteção da página, do layout ou do middleware.

- Porque: os dois são endpoints públicos, chamáveis direto, fora da tela que os usa.
- Como: o schema é o mesmo do formulário (`ia/regras/tanstack.md › T3`).

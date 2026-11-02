# Interface

> Para: todos os papéis · Leia quando: arquivo `.tsx`, `.jsx` ou de estilos, ou arquivo com texto exibido ao usuário, ícone ou animação.

## Fontes

- Nenhuma registrada. Entra aqui, conferida no destino, a fonte global de estilos ou tema que define a tipografia (UI-6).

## Regras

### UI-1: Primitivo de interface usa Base UI sempre que a biblioteca tem um componente equivalente, inclusive para controle nativo como botão.

- Por quê: comportamento e acessibilidade iguais em toda a interface.

### UI-2: Transição de componente Base UI usa primeiro os mecanismos documentados da biblioteca; os demais movimentos usam Motion quando compatível.

- Por quê: preservar o ciclo de vida dos componentes e evitar duas soluções concorrentes de animação.
- Como: na integração, preserve foco, eventos e montagem e desmontagem; respeite a preferência por movimento reduzido.

### UI-3: Medida fixa de layout, espaçamento, raio e comprimento de sombra é múltiplo de 4px.

- Por quê: escala visual consistente, mesmo quando o design recebido usa outra.
- Escopo: a tipografia segue UI-6.
- Exceção: caso técnico pontual, como borda fina, decidido por necessidade e justificado nas `Decisões` do relato e na entrega.

### UI-4: Opacidade de cor é múltiplo de 0,1 (10%).

- Por quê: escala de transparência previsível.

### UI-5: Duração e atraso são múltiplos de 0,25s (250ms), incluindo zero.

- Por quê: ritmo consistente entre transições, animações e demais temporizações.

### UI-6: Tipografia é definida na fonte global de estilos ou no tema, por elemento semântico ou classe de contexto, com os tokens oficiais de tamanho do Tailwind e as alturas de linha deles.

- Por quê: ajuste global num lugar só e texto previsível.
- Como:
  - Sem tamanho avulso, altura de linha manual nem sobrescrita local de tamanho ou de altura de linha.
  - Espaçamento entre letras usa os tokens oficiais `tracking-*` do Tailwind; nunca `letter-spacing` avulso.
- Fonte: a fonte global de estilos ou tema, em `Fontes`; a configuração segue a versão instalada.

### UI-7: Espaço entre elementos usa `gap` no contêiner.

- Por quê: separação explícita e fácil de depurar.
- Como: não use margem nem `space-*` para separar elementos; `padding` é o espaço interno.

### UI-8: Classes Tailwind ficam inline no `className`, inclusive dentro de `twMerge` e das expressões que ramificam a aparência, sempre que possível.

- Por quê: o autocomplete do Tailwind funciona, e a aparência fica visível junto do elemento que ela estiliza.

### UI-9: Ícone da interface vem de `lucide-react`.

- Por quê: linguagem visual única, sem redesenhar símbolos que a biblioteca já oferece.

### UI-10: Classes de mais de uma parte (condicionais, props ou variáveis) se combinam com `twMerge`; nunca com template literal, `+` ou `join`.

- Por quê: conflito entre utilidades resolvido de forma previsível e uma só forma de compor classes.

### UI-11: Texto exibido ao usuário em português do Brasil.

- Por quê: a interface fala o idioma de quem a usa.
- Escopo: rótulos, mensagens (inclusive de validação e de erro), texto alternativo e atributos de acessibilidade como `alt` e `aria-label`, título e metadados da página.

## Padrões

- Nenhum registrado.

## Armadilhas

- Nenhuma registrada.

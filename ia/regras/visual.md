# Visual

## Regras

### V1 · Primitivos do Base UI

Primitivo de interface usa Base UI sempre que a biblioteca tem um componente equivalente, inclusive para controle nativo como botão.

- Porque: comportamento e acessibilidade iguais em toda a interface.

### V2 · Animação

Transição de componente Base UI usa primeiro os mecanismos documentados da biblioteca. Os demais movimentos usam Motion, quando compatível.

- Porque: preserva o ciclo de vida dos componentes e evita duas soluções concorrentes de animação.
- Como: na integração, preserve foco, eventos e montagem e desmontagem; respeite a preferência por movimento reduzido.

### V3 · Medidas em múltiplos de 4px

Medida fixa de layout, espaçamento, raio e comprimento de sombra é múltiplo de 4px.

- Porque: escala visual consistente, mesmo quando o design recebido usa outra.
- Vale para: tudo menos a tipografia, que segue V6.
- Exceto: caso técnico pontual, como borda fina, decidido por necessidade e justificado nas `Escolhas` do retorno e na entrega.

### V4 · Opacidade em múltiplos de 10%

Opacidade de cor é múltiplo de 0,1 (10%).

- Porque: escala de transparência previsível.

### V5 · Tempo em múltiplos de 250ms

Duração e atraso são múltiplos de 0,25s (250ms), incluindo zero.

- Porque: ritmo consistente entre transições, animações e demais temporizações.

### V6 · Tipografia no tema

Tipografia é definida na fonte global de estilos ou no tema, por elemento semântico ou classe de contexto, com os tokens oficiais de tamanho do Tailwind e as alturas de linha deles.

- Porque: ajuste global num lugar só e texto previsível.
- Como:
  - Sem tamanho avulso, altura de linha manual nem sobrescrita local de tamanho ou de altura de linha.
  - Espaçamento entre letras usa os tokens oficiais `tracking-*` do Tailwind. Nunca `letter-spacing` avulso.
- Fonte: a fonte global de estilos ou o tema, na configuração da versão instalada. Registre o caminho aqui quando existir.

### V7 · Espaço com `gap`

Espaço entre elementos usa `gap` no contêiner.

- Porque: separação explícita e fácil de depurar.
- Como: não use margem nem `space-*` para separar elementos. `padding` é o espaço interno.

### V8 · Classes inline

Classes Tailwind ficam inline no `className`, inclusive dentro de `twMerge` e das expressões que ramificam a aparência, sempre que possível.

- Porque: o autocomplete do Tailwind funciona, e a aparência fica visível junto do elemento que ela estiliza.

### V9 · Ícones do Lucide

Ícone da interface vem de `lucide-react`.

- Porque: linguagem visual única, sem redesenhar símbolos que a biblioteca já oferece.

### V10 · Classes combinadas com `twMerge`

Classes de mais de uma parte (condicionais, props ou variáveis) se combinam com `twMerge`. Nunca com template literal, `+` ou `join`.

- Porque: conflito entre utilidades resolvido de forma previsível, e uma só forma de compor classes.

### V11 · Texto em português

Texto exibido ao usuário é em português do Brasil.

- Porque: a interface fala o idioma de quem a usa.
- Vale para: rótulos, mensagens (inclusive de validação e de erro), texto alternativo e atributos de acessibilidade como `alt` e `aria-label`, título e metadados da página.

## Moldes

Nenhum.

## Alertas

Nenhum.

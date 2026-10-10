# Padrões e decisões

> Os exemplares a seguir e as decisões que outras tarefas precisam repetir igual. O orquestrador mantém este arquivo como parte das entregas, a partir do que os implementadores sinalizam em `Registro:`; o humano vê as mudanças no diff e pode vetá-las ao aceitar. Não é norma: dá para desviar quando a tarefa justifica, e então a entrada é atualizada.

Entra aqui:

- a primeira instância de algo que vai se repetir e em que divergir quebraria a consistência;
- uma decisão que outras tarefas precisam repetir igual;
- qual de duas formas existentes no código é a atual.

Não entra: o que o código já mostra sem ambiguidade, o que uma norma ou uma checagem já garante, uma escolha local.

Formato, uma linha por entrada:

```markdown
- Formulário com validação: `src/conta/perfil-form.tsx`. Schema junto do formulário; mensagens vêm de `src/i18n/`.
- Links de arquivos públicos: `/arquivos/<slug>`; o slug não muda quando o arquivo é substituído.
```

<!-- As entradas do projeto entram abaixo, agrupadas por área quando forem várias. -->

- Bibliotecas: as dependências de `package.json` resolvem, sozinhas ou combinadas, as necessidades que cobrem, conforme a documentação oficial vinculada no `README.md`; não escrever solução própria para elas.
- Configuração própria do ESLint por assunto: `eslint/imports/index.mjs`. Cada grupo exporta uma configuração e é composto em `eslint.config.mjs`; usar como exemplar para novos grupos.
- Tipografia global: `src/app/globals.css`. Estilos semânticos na camada `base`; variações de contexto, quando necessárias, na camada `components`.
- Primitivos Base UI: `src/components/button/index.tsx`. Preservar props, ref e composição da biblioteca; combinar classes com `tailwind-merge`, incluindo callbacks de estado. Em ações assíncronas, manter foco e nome acessível explícito durante o carregamento.
- Campos de formulário: `src/components/input/index.tsx`. Envolver o controle Base UI em `FormField` (rótulo, descrição, erro e loading) e a caixa em `FieldBox`, com ícones em `FieldSlot`; os estados visuais da caixa vêm dos atributos de dados da raiz do campo.
- Testes de componentes: `src/components/button/index.test.tsx`. Consultar pelo papel e nome acessível e interagir como o usuário.
- Estratégia de testes: unitários para comportamento isolado; e2e para fluxos reais da aplicação ou riscos que exigem navegador. A disponibilidade da ferramenta, sozinha, não justifica criar uma suíte.
- Sobreposições: `src/components/dialog/dialog-content/index.tsx`. Vidro reservado a uma única camada flutuante; superfícies de trabalho permanecem sólidas.
- Notificações: `src/components/toast/toast-provider/index.tsx` monta o viewport; consumidores usam `src/components/toast/use-toast/index.tsx` dentro do provider para adicionar, atualizar e fechar notificações.
- Formulários guiados pelo schema: `src/components/dynamic-entry-form/index.tsx`. TanStack Form coordena validação e submissão com os schemas Zod de `src/components/dynamic-entry-form/schema.ts` via Standard Schema; os controles são escolhidos pelo tipo de campo e compostos com os primitivos existentes.
- Seleção e validação de arquivos locais: `src/components/file-upload/index.tsx`. React Dropzone coordena o seletor e o arraste, composto com os controles existentes; um lote com arquivo inválido é rejeitado por inteiro.
- Seleção contextual de arquivos: `src/components/asset-picker/index.tsx`. O diálogo mantém uma seleção provisória, identifica a origem e aplica o arquivo somente na confirmação.
- Seleção de cores: `src/components/color-picker/index.tsx`. React Colorful coordena a área de cor e a matiz; o controle preserva HEX, RGB, variáveis do tema e opacidade em `ColorValue`, incluindo a matiz escolhida em cores neutras.
- Prévias de dados de integrações: `src/components/json-preview/safe-json.ts`. A mesma representação com segredos ocultos e limites de tamanho é usada para exibir e copiar o JSON.

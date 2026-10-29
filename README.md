# Prisma Tools — site responsivo e PWA

Central expansível de ferramentas web inspirada na categoria de portais de utilidades online. Projeto original, sem banco de dados e com processamento local no navegador.

## Recursos incluídos
- Interface responsiva para desktop, tablet e celular.
- PWA instalável com `manifest.webmanifest`, ícone e service worker para cache/offline.
- Busca instantânea e filtros por categoria.
- Tema claro/escuro (preferência guardada localmente).
- Geradores: CPF/CNPJ sintéticos para testes, nomes fictícios, senhas, UUID, números aleatórios e e-mails `example.com`.
- Validadores: CPF, CNPJ, formato de e-mail e análise indicativa de senha.
- Calculadoras: porcentagem, regra de três e IMC.
- Desenvolvedores: formatador JSON, Base64, codificador de URL, conversor HEX/RGB e timestamp.
- Texto: Lorem Ipsum, caixa de texto, contador de caracteres/palavras e slug.
- Copiar resultado, limpar formulário e mensagens de erro.

## Executar localmente
A PWA e o service worker precisam de HTTP/HTTPS (não abra apenas o `index.html` por `file://`).

### Opção 1 — Python
1. Extraia o ZIP.
2. Abra o terminal na pasta `prisma_tools_pwa`.
3. Execute `python -m http.server 8000`.
4. Acesse `http://localhost:8000`.

### Opção 2 — Node.js
Execute `npx serve .` dentro da pasta e abra o endereço mostrado.

## Publicar gratuitamente
### GitHub Pages
1. Crie um repositório no GitHub e envie todos os arquivos desta pasta.
2. Em **Settings → Pages**, selecione a branch principal e a pasta raiz.
3. Aguarde a publicação. O site será servido em HTTPS e a PWA poderá ser instalada em navegadores compatíveis.

### Netlify / Cloudflare Pages
Crie um novo projeto, envie a pasta ou conecte o repositório Git. Não é necessário comando de build: a raiz publicada contém `index.html`.

## Como adicionar uma ferramenta
No `app.js`, adicione um objeto ao array `tools`. Propriedades:
- `id`: identificador único.
- `n`: nome; `d`: descrição; `c`: categoria; `i`: ícone.
- `f`: lista de campos no formato `[nome, rótulo, tipo, valorInicial]`.
- `run(v)`: função que retorna o resultado. `v` contém os valores dos campos.

Tipos de campo aceitos: `text`, `number`, `email`, `password`, `textarea`, `checkbox` e `select`. Para opções de `select`, passe um quinto argumento com itens no formato `valor|Rótulo`.

## Privacidade e limitações
- Este projeto não usa API, backend, analytics ou banco de dados. Os dados digitados ficam no navegador enquanto a página está aberta.
- A validação de CPF/CNPJ confere formato e dígitos verificadores, mas não confirma existência, titularidade ou situação cadastral.
- Os geradores de documentos são para testes de software. Não use os resultados para se passar por outra pessoa, abrir contas ou realizar cadastros reais.
- A análise de senha é apenas indicativa; não transmite nem armazena a senha.
- O cache offline é atualizado quando o service worker é atualizado. Para alterações futuras, incremente a versão `CACHE` em `sw.js`.
- O botão de instalação aparece em navegadores que suportam o evento de instalação. O comportamento varia entre navegadores e sistemas operacionais.

## Estrutura
- `index.html` — estrutura da aplicação
- `styles.css` — identidade visual e responsividade
- `app.js` — catálogo e lógica das ferramentas
- `manifest.webmanifest` — metadados PWA
- `sw.js` — cache e suporte offline
- `assets/icon.svg` — ícone do aplicativo
